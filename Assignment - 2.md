# Week 2 Assignment

# 2696. Minimum String Length After Removing Substrings
# Solution link : https://leetcode.com/problems/minimum-string-length-after-removing-substrings/submissions/1889532091

# Code:
```
class Solution {
    public int minLength(String s) {
        Stack<Character> stk = new Stack<>();
        for(char c: s.toCharArray()){
            if(c == 'B'){
                if(!stk.isEmpty() && stk.peek() == 'A'){
                    stk.pop();
                }
                else{
                    stk.push(c);
                }
            }
            else if(c == 'D'){
                if(!stk.isEmpty() && stk.peek() == 'C'){
                    stk.pop();
                }
                else{
                    stk.push(c);
                }
            }
            else{
                stk.push(c);
            }
        }
        return stk.size();
    }
}
```

# 1544. Make The String Great
# Solution Link : https://leetcode.com/problems/make-the-string-great/submissions/1889558565

# Code:
```
class Solution {
    public String makeGood(String s) {
        StringBuilder res = new StringBuilder();
        int n = s.length();
        Stack<Character> stk = new Stack<>();
        for(char c: s.toCharArray()){
            if(!stk.isEmpty() && (Math.abs(stk.peek() - c) == 32)){
                stk.pop();
            }
            else stk.push(c);
        }
        while(!stk.isEmpty()){
            res.append(stk.pop());
        }
        res.reverse();
        return res.toString();
    }
}
```

# 907. Sum of Subarray Minimums
# Solution Liink : https://leetcode.com/problems/sum-of-subarray-minimums/submissions/1630010078

# Code:
```
class Solution {
    public int[] findnse(int[]arr, int n){
        int nse[] = new int[n];
        Stack<Integer> st = new Stack<>();
        for(int i = n - 1; i >= 0; i--){
            while(!st.isEmpty() && arr[st.peek()] >= arr[i]){
                st.pop();
            }
            nse[i] = st.isEmpty() ? n: st.peek();
            st.push(i);
        }
        return nse;
    }
    public int[] findpse(int[] arr, int n){
        int[] pse = new int[n];
        Stack<Integer> st = new Stack<>();
        for(int i = 0; i < n; i++){
            while(!st.isEmpty() && arr[st.peek()] > arr[i]){
                st.pop();
            }
            pse[i] = st.isEmpty()? -1: st.peek();
            st.push(i);
        }
        return pse;
    }
    public int sumSubarrayMins(int[] arr) {
        int n = arr.length;
        int nse[] = findnse(arr, n);
        int pse[] = findpse(arr, n);
        long total = 0;
        int mod = (int)(1e9 + 7);
        for(int i = 0; i < n; i++){
            int left = i - pse[i];
            int right = nse[i] - i;
            total = (total + (right * left * 1L* arr[i]) % mod) % mod;
        }
        return (int)total;
    }
}
```

# 1856. Maximum Subarray Min-Product
# Solution Link : https://leetcode.com/problems/maximum-subarray-min-product/submissions/1890938131

# Code:
```
class Solution {
    public int[] func_pse(int[] arr){
        int n = arr.length;
        int[] ans = new int[n];
        Stack<Integer> stk = new Stack<>();
        for(int i = 0; i < n; i++){
            while(!stk.isEmpty() && arr[stk.peek()] >= arr[i]){
                stk.pop();
            }
            ans[i] = stk.isEmpty() ? -1: stk.peek();
            stk.push(i);
        }
        return ans;
    }
    public int[] func_nse(int[] nums){
        int n = nums.length;
        int[] ans = new int[n];
        Stack<Integer> stk = new Stack<>();
        for(int i = n - 1; i >= 0; i--){
            while(!stk.isEmpty() && nums[stk.peek()] > nums[i]){
                stk.pop();
            }
            ans[i] = stk.isEmpty() ? n : stk.peek();
            stk.push(i);
        }
        return ans;
    }
    public int maxSumMinProduct(int[] nums) {
        long max_product = 0;
        int n = nums.length;
        int[] pse = func_pse(nums);
        int[] nse = func_nse(nums);
        long[] pref = new long[n + 1];
        for(int i = 0; i < n; i++){
            pref[i + 1] = pref[i]+ nums[i];
        }
        for(int i = 0; i < n; i++){
            long sum = pref[nse[i]] - pref[pse[i] + 1];
            max_product = Math.max(nums[i] * sum, max_product);
        }
        return (int)(max_product % 1000000007);
    }
}
```

# 1526. Minimum Number of Increments on Subarrays to Form a Target Array
# Solution Link : https://leetcode.com/problems/minimum-number-of-increments-on-subarrays-to-form-a-target-array/submissions/1891785001

# Code: 
```
class Solution {
    public int minNumberOperations(int[] target) {
        int cnt = 0;
        int n = target.length;
        cnt += target[0];
        for(int i = 1; i < n; i++){
            cnt += Math.max(0, target[i] - target[i - 1]);
        }
        return cnt;
    }
}
```

# 2030. Smallest K-Length Subsequence With Occurrences of a Letter
# Solution Link : https://leetcode.com/problems/smallest-k-length-subsequence-with-occurrences-of-a-letter/submissions/1891999170

# Code: 
```
class Solution {
    public String smallestSubsequence(String s, int k, char letter, int repetition) {
        Stack<Character> stk = new Stack<>();
        int n = s.length();

        int remaining = 0;
        for (char c : s.toCharArray()) {
            if (c == letter) remaining++;
        }

        int used = 0;

        for (int i = 0; i < n; i++) {
            char c = s.charAt(i);

            while (!stk.isEmpty()
                    && stk.peek() > c
                    && stk.size() - 1 + (n - i) >= k
                    && (stk.peek() != letter || used - 1 + remaining >= repetition)) {

                char removed = stk.pop();
                if (removed == letter) used--;
            }

            if (stk.size() < k) {
                if (c == letter) {
                    stk.push(c);
                    used++;
                } else {
                    if (k - stk.size() > repetition - used) {
                        stk.push(c);
                    }
                }
            }

            if (c == letter) remaining--;
        }

        StringBuilder ans = new StringBuilder();
        for (char c : stk) ans.append(c);
        return ans.toString();
    }
}
```
