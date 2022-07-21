# LFU Cache

Design and implement a Least Frequently Used(LFU) Cache, to implement the following functions:

```
1. put(U__ID, value): Insert the value in the cache if the key(‘U__ID’) is not already present or update the value of the given key if the key is already present. When the cache reaches its capacity, it should invalidate the least frequently used item before inserting the new item.

2. get(U__ID): Return the value of the key(‘U__ID’),  present in the cache, if it’s present otherwise return -1.
```

### Doubly linked list + map

### Code

```cpp
#include <bits/stdc++.h>

class LFUCache {

    map<int, pair<int, int>> mp; // key, value = {value, frequency}
    map<int, list<int>::iterator> address; // key, address
    list<int> lfu; // doubly linked list to store the order of the keys
    int cap; // total capacity of the cache
    int siz; // current size of the cache
    int freq; // current frequency of the cache
    int minFreq; // minimum frequency of the cache

public:
    LFUCache(int capacity)
    {
        cap = capacity;
        siz = 0;
        freq = 0;
        minFreq = 0;
    }

    int get(int key)
    {
        // if key is not present in the cache, return -1
        if (mp.count(key) == 0) return -1;

        // update the frequency of the key
        mp[key].second++;
        freq = mp[key].second;
        if (freq == minFreq) {
            minFreq++;
        }
        return mp[key].first; // return the value of the key
    }

    void put(int key, int value)
    {
        // if key is not present in the cache, add it to the cache
        if (mp.count(key) == 0) {
            if (siz == cap) {
                // if the cache is full, remove the least frequently used key
                int k = lfu.back();
                lfu.pop_back();
                mp.erase(k);
                address.erase(k);
                siz--;
            }
            lfu.push_front(key);
            address[key] = lfu.begin();
            mp[key] = {value, 1};
            siz++;
            freq = 1;
            minFreq = 1;
        } else {
            // if key is present in the cache, update the value and frequency
            mp[key].first = value;
            mp[key].second++;
            freq = mp[key].second;
            if (freq == minFreq) {
                minFreq++;
            }
        }
    }
};
```

### Alternate Solution

### Code

```cpp
struct Node {
    int key, value, cnt;
    Node* next;
    Node* prev;
    Node(int _key, int _value)
    {
        key = _key;
        value = _value;
        cnt = 1;
    }
};
struct List {
    int size;
    Node* head;
    Node* tail;
    List()
    {
        head = new Node(0, 0);
        tail = new Node(0, 0);
        head->next = tail;
        tail->prev = head;
        size = 0;
    }

    void addFront(Node* node)
    {
        Node* temp = head->next;
        node->next = temp;
        node->prev = head;
        head->next = node;
        temp->prev = node;
        size++;
    }

    void removeNode(Node* delnode)
    {
        Node* delprev = delnode->prev;
        Node* delnext = delnode->next;
        delprev->next = delnext;
        delnext->prev = delprev;
        size--;
    }
};
class LFUCache {
    map<int, Node*> keyNode;
    map<int, List*> freqListMap;
    int maxSizeCache;
    int minFreq;
    int curSize;

public:
    LFUCache(int capacity)
    {
        maxSizeCache = capacity;
        minFreq = 0;
        curSize = 0;
    }
    void updateFreqListMap(Node* node)
    {
        keyNode.erase(node->key);
        freqListMap[node->cnt]->removeNode(node);
        if (node->cnt == minFreq && freqListMap[node->cnt]->size == 0) {
            minFreq++;
        }

        List* nextHigherFreqList = new List();
        if (freqListMap.find(node->cnt + 1) != freqListMap.end()) {
            nextHigherFreqList = freqListMap[node->cnt + 1];
        }
        node->cnt += 1;
        nextHigherFreqList->addFront(node);
        freqListMap[node->cnt] = nextHigherFreqList;
        keyNode[node->key] = node;
    }

    int get(int key)
    {
        if (keyNode.find(key) != keyNode.end()) {
            Node* node = keyNode[key];
            int val = node->value;
            updateFreqListMap(node);
            return val;
        }
        return -1;
    }

    void put(int key, int value)
    {
        if (maxSizeCache == 0) {
            return;
        }
        if (keyNode.find(key) != keyNode.end()) {
            Node* node = keyNode[key];
            node->value = value;
            updateFreqListMap(node);
        } else {
            if (curSize == maxSizeCache) {
                List* list = freqListMap[minFreq];
                keyNode.erase(list->tail->prev->key);
                freqListMap[minFreq]->removeNode(list->tail->prev);
                curSize--;
            }
            curSize++;
            // new value has to be added who is not there previously
            minFreq = 1;
            List* listFreq = new List();
            if (freqListMap.find(minFreq) != freqListMap.end()) {
                listFreq = freqListMap[minFreq];
            }
            Node* node = new Node(key, value);
            listFreq->addFront(node);
            keyNode[key] = node;
            freqListMap[minFreq] = listFreq;
        }
    }
};
```
