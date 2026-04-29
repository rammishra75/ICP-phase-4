# 3D DP Question:

```
class Solution {
    public long func(int ind, int prev, int cnt, long[][][] dp, String s){
        if(cnt == 0 ) return 1;
        if(ind < 0) return 0;
        int prevInd = prev + 1;
        if(dp[ind][prevInd][cnt] != -1) return dp[ind][prevInd][cnt];
        long take = 0;
        int curr = s.charAt(ind) - '0';
        if (prev == -1 || curr != prev) {
            take = func(ind - 1, curr, cnt - 1, dp, s);
        }
        long notTake = func(ind - 1, prev, cnt, dp, s);
        return dp[ind][prevInd][cnt] = take + notTake;
    }
    public long numberOfWays(String s) {
        int n = s.length();
        long[][][] dp = new long[n][3][4];
        for(long[][] a: dp){
            for(long[] b : a){
                Arrays.fill(b, -1);
            }
        }
        return func(n - 1, -1, 3, dp, s);

    }
}
```
