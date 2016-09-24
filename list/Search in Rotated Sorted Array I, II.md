```
Search in Rotated Sorted Array I

Suppose a sorted array is rotated at some pivot unknown to you beforehand.
(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).
You are given a target value to search. If found in the array return its index, otherwise return -1.
You may assume no duplicate exists in the array.
```

To search in a sorted array, remind us of binary-search. 然后这不是一个完全有序而是有序数组旋转过的，折半后，分成的2个区间，其中一个是有序的，另外一个则不是。

```
int search(const vector<int>& nums, int target) {
   int first = 0, last = nums.size();
   while (first != last) {
     const int mid = first + (last - first) / 2;
     if (nums[mid] == target)
        return mid;
     // 从有序的那个子区间着手！如果不在这个有序子区间的范围里，就必定要在另外一个子区间去找     
     if (nums[first] <= nums[mid]) { //[first ,mid] is a sorted array
           if (nums[first] <= target && target < nums[mid])
               last = mid;
           else
               first = mid + 1;
     }
      else {                        //[end ,last] is a sorted array
          if (nums[mid] < target && target <= nums[last-1])
               first = mid + 1;
          else
               last = mid;
         }
     }
     return -1;
}
```

```
Search in Rotated Sorted Array II

Follow up for "Search in Rotated Sorted Array":
What if duplicates are allowed?
Would this affect the run-time complexity? How and why?
Write a function to determine if a given target is in the array.
```

```
通过<=判断一个区间是否是有序区间就不行了，可以拆分成 用<判断是否有序子区间
，用=表示是重复元素，可以跳过重复元素

bool search(const vector<int>& nums, int target) {
   int first = 0, last = nums.size();
   while (first != last) {
       const int mid = first + (last - first) / 2;
      if (nums[mid] == target)
         return true;
      if (nums[first] < nums[mid]) {
         if (nums[first] <= target && target < nums[mid])
             last = mid;
         else
             first = mid + 1;
      } else if (nums[first] > nums[mid]) {
         if (nums[mid] < target && target <= nums[last-1])
             first = mid + 1;
         else
             last = mid;
      } else
          //skip duplicate one
         first++;
    }
    return false;
}
```
Refer :

  
