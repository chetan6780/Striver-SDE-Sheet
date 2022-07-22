# Longest Common Prefix

You are given an array ‘ARR’ consisting of ‘N’ strings. Your task is to find the longest common prefix among all these strings. If there is no common prefix, you have to return an empty string.
A prefix of a string can be defined as a substring obtained after removing some or all characters from the end of the string.

### vertical scan

### Code

```cpp
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        sort(strs.begin(),strs.end());
        string temp = strs[0],res = "";
        int n = temp.size();
        for(int i = 0;i<n; i++){
            for(auto x:strs){
                if(x[i]!=temp[i]){
                    return res;
                }
            }
                res+=temp[i];
        }
        return res;
    }
};
```

### Codestudio

### Code

```cpp
string longestCommonPrefix(vector<string>& arr, int n)
{
    string ans = "";
    for (int i = 0; i < arr[0].length(); i++)
    {
        char ch = arr[0][i];
        for (int j = 1; j < n; j++)
        {
            if (arr[j][i] != ch)
                return ans;
        }
        ans += ch;
    }
    return ans;
}
```
