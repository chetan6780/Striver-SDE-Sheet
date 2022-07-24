# Compare Version Numbers

Given two version numbers, version1 and version2, compare them.

Version numbers consist of one or more revisions joined by a dot '.'. Each revision consists of digits and may contain leading zeros. Every revision contains at least one character. Revisions are 0-indexed from left to right, with the leftmost revision being revision 0, the next revision being revision 1, and so on. For example 2.5.33 and 0.1 are valid version numbers.

To compare version numbers, compare their revisions in left-to-right order. Revisions are compared using their integer value ignoring any leading zeros. This means that revisions 1 and 001 are considered equal. If a version number does not specify a revision at an index, then treat the revision as 0. For example, version 1.0 is less than version 1.1 because their revision 0s are the same, but their revision 1s are 0 and 1 respectively, and 0 < 1.

Return the following:

-   If version1 < version2, return -1.
-   If version1 > version2, return 1.
-   Otherwise, return 0.

### split and compare (two pass)

-   split both strings on '.' and store numbers in vectors.
-   compare each element and return the ans.
-   **TC: O(N)**, N=length of `max(version1, version2)`
-   **SC: O(N)**, N=length of `max(vector1, vector2)`

### Code

```cpp
class Solution {
private:
    vector<int> split(vector<int>& ans, string& s, char ch)
    {
        string temp = "0";
        for (auto x : s) {
            if (x != '.') {
                temp += x;
            } else {
                ans.push_back(stoi(temp));
                temp = "0";
            }
        }
        ans.push_back(stoi(temp));
        return ans;
    }

public:
    int compareVersion(string version1, string version2)
    {
        vector<int> v1, v2;
        // split strings on '.'
        v1 = split(v1, version1, '.');
        v2 = split(v2, version2, '.');

        int n1 = v1.size(), n2 = v2.size();
        int mn = min(n1, n2); // get min length of 2 vectors

        // compare each element up to mn
        for (int i = 0; i < mn; i++) {
            if (v1[i] > v2[i]) {
                return 1;
            } else if (v1[i] < v2[i]) {
                return -1;
            }
        }
        // if vector1 has more elements
        if (n1 > n2) {
            for (int i = mn; i < n1; i++) {
                if (v1[i] > 0) {
                    return 1;
                }
            }
        } else if (n1 < n2) { // if vector2 has more elements
            for (int i = mn; i < n2; i++) {
                if (v2[i] > 0) {
                    return -1;
                }
            }
        }
        return 0;
    }
};
```

### Codestudio

```cpp
int compareVersions(string a, string b)
{
    int i = 0, j = 0, aLen = a.size(), bLen = b.size();
    while (i < aLen || j < bLen) {
        long long n1 = 0, n2 = 0;
        while (i < aLen && a[i] != '.') {
            n1 = n1 * 10 + 1ll * (a[i] - '0');
            i++;
        }
        while (j < bLen && b[j] != '.') {
            n2 = n2 * 10 + 1ll * (b[j] - '0');
            j++;
        }
        if (n1 < n2)
            return -1;
        else if (n1 > n2)
            return 1;
        i++;
        j++;
    }
    return 0;
}
```