# Max Valid Pair Sum

```
public class Solution {
    public int maxValidPairSum(int[] nums, int k) {
        int maxSum = Integer.MIN_VALUE;
        int maxI = Integer.MIN_VALUE;
        
        // Iterate through all possible right elements
        for (int j = k; j < nums.length; j++) {
            // Update the maximum valid left element available for this j
            maxI = Math.max(maxI, nums[j - k]);
            // Update the overall maximum pair sum
            maxSum = Math.max(maxSum, maxI + nums[j]);
        }
        
        return maxSum;
    }
}

```
