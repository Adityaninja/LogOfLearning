# 24th July

1) Question:Given the root of a binary tree, return the same tree where every subtree (of the given tree) not containing a 1 has been removed. A subtree of a node node is node plus every node that is a descendant of node.

Input: root = \[1,null,0,0,1]
Output: \[1,null,0,null,1]

Explanation:
Only the red nodes satisfy the property "every subtree not containing a 1".
The diagram on the right represents the answer.

``` python
def pruneTree(self, root):
    result = self.recursive_approach(root)
    return root if result is False else None

def recursive_approach(self, root):
    if root is None:
        return True

    if self.recursive_approach(root.left):
        root.left = None

    if self.recursive_approach(root.right):
        root.right = None

    return root.val != 1 and not root.left and not root.right

```

Notes: Pretty straightforward, returning true means it is good for deletion. One observation was that the run time changes significantly just by removing an extra variable and removing a few lines of code


2.Given a sorted integer array arr, two integers k and x, return the k closest integers to x in the array. The result should also be sorted in ascending order.

An integer a is closer to x than an integer b if:

|a - x| < |b - x|, or
|a - x| == |b - x| and a < b


Example 1:

Input: arr = \[1,2,3,4,5], k = 4, x = 3
Output: \[1,2,3,4]
Example 2:

Input: arr = \[1,2,3,4,5], k = 4, x = -1
Output: \[1,2,3,4]

- Approach 1: In the first approach we sort the elements with the comparator as abs(x-num) and then choose the first k elements and then resort. The complexity is o(nlog(n)) + O(klog(k))
We learnt the way to sort is sorted(arr, key = lambda num: abs(x-num)). The constraint of the smallest element being picked is automatically satisfied as  
I think the sorted takes care of that for us in the it prefers the leftmost element if the value of the keys are the same.

``` python
class Solution:
    def pruneTree(self, root):
        result = self.recursive_approach(root)
        return root if result is False else None

    def recursive_approach(self, root):
        if root is None:
            return True

        if self.recursive_approach(root.left):
            root.left = None

        if self.recursive_approach(root.right):
            root.right = None

        return root.val != 1 and not root.left and not root.right
 ```

- Approach 2: In the second approach, we do a binary search for the smallest element <= the input element. This is done by bisect.bisect_left(arr, x). Now the left and right boundaries start from here.
  Note the subtle left = bisect.bisect_left(arr, x) - 1 and right = left + 1. We do not include the left and the right boundaries in the k-element answer as we do not know which of left/right to include at this point.

``` python
import bisect

def findClosestElements(self, arr, k, x):
    # return self.sorting_approach(arr, k, x)
    return self.bin_search_sliding_window(arr, k, x)

def bin_search_sliding_window(self, arr, k, x):
    if k == len(arr):
        return arr

    left_index = bisect.bisect_left(arr, x) - 1
    right_index = left_index + 1

    while right_index - left_index - 1 < k:
        if left_index == -1:
            right_index += 1
            continue
    
        if right_index == len(arr):
            left_index -= 1
            continue

        if self.find_closer_index(arr, left_index, right_index, x) == left_index:
            left_index -= 1

        else:
            right_index += 1
    return arr[left_index+1: right_index]

def find_closer_index(self, arr, left_index, right_index, x):
    return left_index if abs(arr[left_index] - x) <= abs(arr[right_index] - x) else right_index

def sorting_approach(self, arr, k, x):
    sorted_arr = sorted(arr, key=lambda num: abs(x - num))
    result = sorted_arr[:k]
    return sorted(result)
```

