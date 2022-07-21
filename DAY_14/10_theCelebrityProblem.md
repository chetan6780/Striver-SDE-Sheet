# The Celebrity Problem

There are ‘N’ people at a party. Each person has been assigned a unique id between 0 to 'N' - 1(both inclusive). A celebrity is a person who is known to everyone but does not know anyone at the party.
Given a helper function ‘knows(A, B)’, It will returns "true" if the person having id ‘A’ know the person having id ‘B’ in the party, "false" otherwise. Your task is to find out the celebrity at the party. Print the id of the celebrity, if there is no celebrity at the party then print -1.

### Solution

### Code

```cpp
/*
	This is signature of helper function 'knows'.
	You should not implement it, or speculate about its implementation.

	bool knows(int A, int B);
	Function 'knows(A, B)' will returns "true" if the person having
	id 'A' know the person having id 'B' in the party, "false" otherwise.
*/

int findCelebrity(int n)
{
    int candidate = 0;
    for (int i = 1; i < n; i++)
    {
        if (knows(candidate, i))
            candidate = i;
    }
    for (int i = 0; i < n; i++)
    {
        if (i != candidate && (knows(candidate, i) || !knows(i, candidate)))
            return -1;
    }
    return candidate;
}
```
