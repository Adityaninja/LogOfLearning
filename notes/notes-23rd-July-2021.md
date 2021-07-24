# 23rd July


Question: Given an array nums, partition it into two (contiguous) subarrays left and right so that:
Every element in left is less than or equal to every element in right.
left and right are non-empty.
left has the smallest possible size.
Return the length of left after such a partitioning.  It is guaranteed that such a partitioning exists.

Input: nums = \[5,0,3,8,6\]
Output: 3
Explanation: left = \[5,0,3\], right = \[8,6\]

Input: nums = \[1,1,1,0,6,12\]
Output: 4
Explanation: left = \[1,1,1,0\], right = \[6,12\]

Solution: The idea is to find the smallest element. The smallest element clearly cannot be in the right set. What prevents us from taking the element uptil the smallest
element as the smallest set? The fact that there might be an element in the left set which is larger than some elements in the
right set. So we traverse the right set to check, meanwhile if we see an element larger than the largest element in left set, then we temporarily note it down as it is possible that this is the largest element in the left set.
``` python

def partitionDisjoint(self, nums):
    lowest_index = None
    for index, number in enumerate(nums):
        if lowest_index is None or nums[lowest_index] > nums[index]:
            lowest_index = index

    highest_left_number_index = None
    for index, number in enumerate(nums[:lowest_index+1]):
        if highest_left_number_index is None or nums[highest_left_number_index] < nums[index]:
            highest_left_number_index = index

    possible_highest_index = highest_left_number_index
    split_index = lowest_index

    if lowest_index + 1 < len(nums):
        for index in range(lowest_index+1, len(nums)):
            if nums[highest_left_number_index] < nums[index]:
                possible_highest_index = index

            elif nums[highest_left_number_index] > nums[index]:
                highest_left_number_index = possible_highest_index
                split_index = index

    return split_index + 1
```
Errors I made:
       for index in range(lowest_index+1, len(nums)):
  This was previously:  
   for index, num in enumerate(nums[lowest_index+1:\]):
   Which is wrong as the index here refers to the list specified whereas we want the indexes of the original array
