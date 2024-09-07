## Step 1: Array+Linkedlist

### LeetCode 26 - Remove Duplicates from Sorted Array

The main task is to delete duplicate elems from array (sorted in non-decreasing order) in place

#### Example:
```c++
vector<int>nums = {1, 1, 2, 3, 3, 4, 5, 5};
removeDuplicates(nums);
nums = {1, 2, 3, 4, 5};
```

#### Solution

```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        // .erase waits for iterator 
        auto it = nums.begin();
        for (int i = 0; i < nums.size() - 1; ++i){
            if (nums[i] == nums[i + 1]){
                nums.erase(it + i + 1);
                --i; // without decrement throws error out of range
            }
        }
        return nums.size();
    }
};
```

### LeetCode 283 - Move Zeroes

Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements (in place)

#### Example:
```c++
vector<int> nums = { 0, 1, 0, 3, 12 };
moveZeroes(nums);
nums = {1, 3, 12, 0, 0};
```

#### Solution

We are using two pointers for tracking indexToWrite (order place for writting non zero elem) and currentIndex to iterate over an array.

Second cycle for writting zeroes.

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int indexToWrite = 0;
        for (int currentIndex = 0; currentIndex < nums.size(); ++currentIndex){
            if (nums[currentIndex] != 0){
                nums[indexToWrite] = nums[currentIndex];
                indexToWrite++;
            }
        }

        for (indexToWrite; indexToWrite < nums.size(); ++indexToWrite){
            nums[indexToWrite] = 0;
        }
    }
};
```