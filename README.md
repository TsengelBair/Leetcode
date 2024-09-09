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

### LeetCode 88 - Merge Sorted Array

Given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.

#### Example:
```c++
Input: nums1 = [1, 2, 3, 0, 0, 0], m = 3, nums2 = [2, 5, 6], n = 3
Output: [1, 2, 2, 3, 5, 6]
```

#### Solution

```c++
class Solution {
public:
    void merge(std::vector<int>& nums1, int m, std::vector<int>& nums2, int n) {
        int indexToWrite = nums1.size() - 1;
        while (m > 0 and n > 0) {
            // will rewrite the last zero in nums1 by the last elem in nums2 
            // (arrays are sorted)
            if (nums1[m - 1] <= nums2[n - 1]) {
                nums1[indexToWrite] = nums2[n - 1];
                n--;
            }
            // if elem from the first array is bigger, we should copy it and place  
            // at the end of first array
            else {
                nums1[indexToWrite] = nums1[m - 1];
                m--;
            }
            indexToWrite--;
        }

        // if there are not checked elems from the second array
        while (n > 0) {
            nums1[indexToWrite] = nums2[n - 1];
            n--;
            indexToWrite--;
        }
    }
};
```
