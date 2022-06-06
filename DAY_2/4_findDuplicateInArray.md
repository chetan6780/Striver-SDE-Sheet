# Find the Duplicate Number

Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.

There is only one repeated number in nums, return this repeated number.

You must solve the problem without modifying the array nums and uses only constant extra space.

### O(N^2) Brute force

-   check for all numbers if duplicate number exists.

### O(NlogN) Sorting

-   Sort the array and duplicate numbers will be next to each other.

### O(N) Time O(N) space, Hash Table

-   With the help of hash (set/map/vector) we can find the duplicate number.

### O(N) Time O(1) space, Floyd's Cycle Detection Algorithm

```cpp
class Solution{
public:
	int findDuplicate(vector<int> &nums){
		int slow = nums[0];
		int fast = nums[0];

		do{
			slow = nums[slow];
			fast = nums[nums[fast]];
		} while (slow != fast);

		fast = nums[0];
		while (slow != fast){
			slow = nums[slow];
			fast = nums[fast];
		}
		return slow;
	}
};
```
