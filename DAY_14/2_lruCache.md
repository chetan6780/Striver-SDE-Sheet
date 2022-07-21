# LRU Cache Implementation

Design and implement a data structure for Least Recently Used (LRU) cache to support the following operations:

```
1. get(key) - Return the value of the key if the key exists in the cache, otherwise return -1.

2. put(key, value), Insert the value in the cache if the key is not already present or update the value of the given key if the key is already present. When the cache reaches its capacity, it should invalidate the least recently used item before inserting the new item.
```

### Implementation using a doubly linked list

-   To implement the LRU cache, we need a **doubly linked list** to store the **`{key, value}`**. A **map** to store **`{key, value}`** and **another map** to store **`{key, address of the node in the list}`**. `cap` is the capacity of the cache and `siz` is the current size of the cache.

1. **Get method:**
    - If the key is **not present** in the cache, **return -1**.
    - If key is **present** in the cache, move the key to the front of the list. _Return the value of the key form map_.
        - To move first **delete** the key from list and its address from map.
        - Then **push key** in front of the list and its **new address** (`lru.begin()`) in map.
2. **Put method:**
    - if key is already present delete it. We will add updated {key, value}
    - if the cache is full, delete the least recently used key
    - Add updated {key, value} to the cache

### Code

```cpp
#include <bits/stdc++.h>

class LRUCache {

    map<int, int> mp; // key, value
    map<int, list<int>::iterator> address; // key, address
    list<int> lru; // doubly linked list to store the order of the keys
    int cap; // total capacity of the cache
    int siz; // current size of the cache

public:
    LRUCache(int capacity)
    {
        cap = capacity;
        siz = 0;
    }

    int get(int key)
    {
        // if key is not present in the cache, return -1
        if (mp.count(key) == 0) return -1;

        // if key is present in the cache, update the order of the key, because just now we've accessed it and now it became the most recent one
        lru.erase(address[key]); // erase the key from the list with help of it's address
        address.erase(key); // erase the address of the key

        lru.push_front(key); // insert the key at the front of the list (most recent)
        address[key] = lru.begin(); // update the address of the key

        return mp[key]; // return the value of the key
    }

    void put(int key, int value)
    {
        // if key is already present delete it. We will add updated {key, value}
        if (mp.count(key) == 1) {
            lru.erase(address[key]); // erase the key from the list with help of it's address
            address.erase(key); // erase the address of the key
            mp.erase(key); // erase the key from the map
            siz--; // decrease the size of the cache
        }

        // if the cache is full, delete the least recently used key
        if (siz == cap) {
            int k = lru.back(); // LRU key
            lru.pop_back(); // remove lru key from the list
            address.erase(k); // remove the address of the lru key
            mp.erase(k); // remove the lru key from the map
            siz--; // decrease the size of the cache
        }

        // Add updated {key, value} to the cache
        lru.push_front(key); // insert the key at the front of the list (most recent)
        address[key] = lru.begin(); // update the address of the key
        mp[key] = value; // update the value of the key
        siz++; // increase the size of the cache
    }
};
```

### Alternate Solution

### Code

```cpp
class LRUCache {
public:
    class node { // doubly linked list node
    public:
        int key;
        int val;
        node* next;
        node* prev;
        node(int _key, int _val)
        {
            key = _key;
            val = _val;
        }
    };

    node* head = new node(-1, -1);
    node* tail = new node(-1, -1);

    int cap;
    unordered_map<int, node*> m;

    LRUCache(int capacity)
    {
        cap = capacity;
        head->next = tail;
        tail->prev = head;
    }

    void addnode(node* newnode)
    {
        node* temp = head->next;
        newnode->next = temp;
        newnode->prev = head;
        head->next = newnode;
        temp->prev = newnode;
    }

    void deletenode(node* delnode)
    {
        node* delprev = delnode->prev;
        node* delnext = delnode->next;
        delprev->next = delnext;
        delnext->prev = delprev;
    }

    int get(int key_)
    {
        if (m.find(key_) != m.end()) {
            node* resnode = m[key_];
            int res = resnode->val;
            m.erase(key_);
            deletenode(resnode);
            addnode(resnode);
            m[key_] = head->next;
            return res;
        }

        return -1;
    }

    void put(int key_, int value)
    {
        if (m.find(key_) != m.end()) {
            node* existingnode = m[key_];
            m.erase(key_);
            deletenode(existingnode);
        }
        if (m.size() == cap) {
            m.erase(tail->prev->key);
            deletenode(tail->prev);
        }

        addnode(new node(key_, value));
        m[key_] = head->next;
    }
};
```
