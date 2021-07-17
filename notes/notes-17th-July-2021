# 17-July-2021

## Given an integer array nums, return the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.

- Brute force O(n**3)
``` python
def brute_force(self, nums):
    count = 0
    if nums is None or len(nums) < 2:
        return 0
    nums.sort()
    for i in range(len(nums)-2):
        for j in range(i+1, len(nums)-1):
            for k in range(j+1, len(nums)):
                if nums[i] + nums[j] > nums[k]:
                    # print(nums[i], nums[j], nums[k])
                    count += 1
    return count
```

- Binary search(O(n**2 log(n))
``` python
def bin_search_method(self, nums):
    nums.sort()
    count = 0
    for i in range(0, len(nums)):
        for j in range(i+1, len(nums)-1):
            result = self.find_least_index_greater_equalto_than_target(nums, j + 1, len(nums) - 1, nums[i] + nums[j])
            if nums[-1] < nums[i] + nums[j]:
                count += (len(nums)-1) - j
            elif result is not None:
                count += (result-1) - j

    return count
    
def find_least_index_greater_equalto_than_target(self, nums, low, high, target):
    if low > high:
        return None

    mid = (low + high) // 2
    if nums[mid] >= target:
        result = self.find_least_index_greater_equalto_than_target(nums, low, mid - 1, target)
        if result is not None:
            return result
        else:
            return mid

    elif nums[mid] < target:
        return self.find_least_index_greater_equalto_than_target(nums, mid + 1, high, target)





```

- Linear scan O(n**2)
``` python
def linear_scan(self, nums):
    nums.sort()
    count = 0
    for i in range(0, len(nums)-2):
        k = i + 2
        for j in range(i+1, len(nums)-1):
            while k < len(nums) and nums[k] < nums[i] + nums[j]:
                k += 1
            count += k - j - 1
    return count
        
```

