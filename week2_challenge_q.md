# Week 2 Challenges questions:

# Question 4: 
# 1574. Shortest Subarray to be Removed to Make Array Sorted
# Solution link : https://leetcode.com/problems/shortest-subarray-to-be-removed-to-make-array-sorted/submissions/1897407367

# Code:
```
class Solution {
    public int findLengthOfShortestSubarray(int[] arr) {
       int n = arr.length;
       int left = 0;
       while(left + 1 < n && arr[left] <= arr[left + 1]){
            left++;
       }
       if(left == n - 1) return 0;
       int right = n - 1;
       while(right > 0 && arr[right - 1] <= arr[right]){
            right--;
       }
       int res = Math.min(n - left - 1, right);
       int i = 0; 
       int j = right;
       while(i <= left && j < n){
            if(arr[i] <= arr[j]){
                res = Math.min(res, j - i - 1);
                i++;
            }
            else j++;
       }
       return res;
    }
}
```

# Question 5
# 3113. Find the Number of Subarrays Where Boundary Elements Are Maximum
# Solution Link : https://leetcode.com/problems/find-the-number-of-subarrays-where-boundary-elements-are-maximum/submissions/1897379980

# Code:
```
class Solution {
    public long numberOfSubarrays(int[] nums) {
        ArrayDeque<int []> stk = new ArrayDeque<>(); 
        long cnt = 0;
        for(int a: nums){
            while(!stk.isEmpty() && stk.peek()[0] < a){
                stk.pop();
            }
            if(stk.isEmpty() || stk.peek()[0] != a){
                stk.push(new int[] {a, 0});
            }
            cnt += ++stk.peek()[1];
        }
        return cnt;
    }
}
```
