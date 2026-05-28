# Largest Palindromic Number

```
class Solution {
    public String largestPalindromic(String num) {
        int[] freq = new int[10];
        for(int n : num.toCharArray()){
            freq[n - '0']++;
        }
        StringBuffer even = new StringBuffer();
        int max = -1;
        for(int i = 9; i >= 0; i--){
            if(freq[i] % 2 == 1){
                max = Math.max(max, i);
            }
            for(int j = 0; j < freq[i] / 2; j++){
                even.append(i);
            }
        }
        String ans = even.toString() + (max == -1 ? "" : max) + even.reverse().toString();
        if(ans.charAt(0) == '0'){
            if(max == -1) return "0";
            return max + "";
        }
        return ans;
    }
}
```
