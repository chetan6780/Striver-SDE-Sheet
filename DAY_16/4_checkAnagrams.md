# Valid Anagram

Given two strings s and t, return true if t is an anagram of s, and false otherwise.

### O(N logN) Time and constant space

-   sort both strings and compare them.
-   if they are equal, return true else false.

### Code

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        sort(s.begin(),s.end());
        sort(t.begin(),t.end());
        return s==t?true:false;
    }
};
```

### O(N) Time and O(N)=O(26) constant space

-   We store frequency of each character in a hash table.
-   Decrement the frequency of each character in hash table which is in the t.
-   If any frequency is not zero, return false.

### Code

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        vector<int> a(26,0);
        if(s.size()!=t.size()) return false;
        for(auto &x:s){
            a[x-'a']++;
        }
        for(auto &x:t){
            --a[x-'a'];
        }
        for(auto &x:a){
            if(x>=1) return false;
        }
        return true;
    }
};
```

### Only 2 loops

-   first confirm sizes of both strings is same.
-   We can avoid 3rd loop by checking if the frequency of each character less than 0 then return false.
-   return true by default.

### Code

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        vector<int> a(26,0);
        if(s.size()!=t.size()) return false;
        for(auto &x:s){
            a[x-'a']++;
        }
        for(auto &x:t){
            if(--a[x-'a']<0) return false;
        }
        return true;
    }
};
```

### Codestudio

```cpp
bool areAnagram(string& str1, string& str2)
{
    if (str1.length() != str2.length())
        return false;
    int count[26] = { 0 };
    for (int i = 0; i < str1.length(); i++) {
        count[str1[i] - 'a']++;
        count[str2[i] - 'a']--;
    }
    for (int i = 0; i < 26; i++) {
        if (count[i] != 0)
            return false;
    }
    return true;
}
```
