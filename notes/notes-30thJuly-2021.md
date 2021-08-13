## 30th July

 You are given an integer array arr. You can choose a set of integers and remove all the occurrences of these integers in the array.

Return the minimum size of the set so that at least half of the integers of the array are removed.



Example 1:

Input: arr = \[3,3,3,3,5,5,5,2,2,7]
Output: 2
Explanation: Choosing {3,7} will make the new array \[5,5,5,2,2] which has size 5 (i.e equal to half of the size of the old array).
Possible sets of size 2 are {3,5},{3,2},{5,2}.
Choosing set {2,7} is not possible as it will make the new array \[3,3,3,3,5,5,5] which has size greater than half of the size of the old array.

Approach 1: Here we first have a counter which is provided by collections.Counter which returns a dictionary with the key as the element and the value as the count.  
And then we get to the number needed by adding up the sorted counts provided by the counter. Complexity is O(n*log(n))

``` python
import collections
import math

class Solution:
    def minSetSize(self, arr) -> int:
        if not arr:
            return 0
        counts = collections.Counter(arr)
        counts_list = [x for x in counts.values()]
        counts_list.sort(reverse=True)

        set_size = 0
        num_elements_to_remove = math.ceil(len(arr)/2)
        for num in counts_list:
            if num_elements_to_remove > 0:
                num_elements_to_remove -= num
                set_size += 1

            else:
                break

        return set_size

```

Approach 2: Here just as the above approach we have a counter but we attempt to sort the count array usign bucket sort. Bucket sort needs an array which is as large as the maximum frequent element which occurs in the array. This can't be larger than 'n' where n is the size of the
array. The counter array here basically represents the counter of the frequency of that number in the original array.

```python
import collections
import math

def minSetSize(self, arr):

    # In Python, we can use the built-in Counter class.
    counts = collections.Counter(arr)
    max_value = max(counts.values())

    # Put the counts into buckets.
    buckets = [0] * (max_value + 1)

    for count in counts.values():
        buckets[count] += 1

    # Determine set_size.
    set_size = 0
    arr_numbers_to_remove = len(arr) // 2
    bucket = max_value
    while arr_numbers_to_remove > 0:
        max_needed_from_bucket = math.ceil(arr_numbers_to_remove / bucket)
        set_size_increase = min(buckets[bucket], max_needed_from_bucket)
        set_size += set_size_increase
        arr_numbers_to_remove -= set_size_increase * bucket
        bucket -= 1

    return set_size

```

