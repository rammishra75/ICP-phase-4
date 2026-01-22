# 121. Best Time to Buy and Sell Stock
## Question_Link : https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/
## Solution_Link : https://leetcode.com/problems/best-time-to-buy-and-sell-stock/submissions/1883660204

## Code 
```
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        int n = prices.length;
        int min  = prices[0];
        for(int i = 1; i < n; i++){
            profit = Math.max(profit, prices[i] - min);
            if(prices[i] < min) min = prices[i];
        }
        return profit;
    }
}


# 28. Find the Index of the First Occurrence in a String
# Solution_link : https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/submissions/1883643196

# Code:

class Solution {
    public int strStr(String haystack, String needle) {
        if(!haystack.contains(needle)) return -1;
        if(haystack.equals(needle)) return 0;
        int n = haystack.length();
        int m = needle.length();
        int strt = -1;
        for(int i = 0; i < n; i++){
            if(haystack.charAt(i) == needle.charAt(0)){
                if(haystack.substring(i, i + m).equals(needle)){
                    strt = i;
                    break;
                }
            }
        }
        return strt;
    }
}


# 15. 3Sum
# Solution_link : https://leetcode.com/problems/3sum/submissions/1556268102

# Code: 

class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        int l = nums.length;
        List<List<Integer>> ans = new ArrayList<>();
        for(int i = 0; i < l; i++){
            if(i > 0 && nums[i] == nums[i - 1]) continue;
            int j = i + 1;
            int k = l - 1;
            while(j < k){
                int sum = nums[i] + nums[j] + nums[k];
                if(sum < 0){
                    j++;
                }
                else if(sum > 0){
                    k--;
                }
                else{
                    List<Integer> temp = Arrays.asList(nums[i],nums[j],nums[k]);
                    ans.add(temp);
                    j++;
                    k--;
                    while(j < k && nums[j] == nums[j - 1]){
                        j++;
                    }
                    while(j < k && nums[k] == nums[k + 1]){
                        k--;
                    }
                }
            }
        }
        return ans;
    }
}


# 204. Count Primes
# Solution_Link : https://leetcode.com/problems/count-primes/submissions/1617419064

# Code:

class Solution {
    public int countPrimes(int n) {
        if(n <= 2) return 0;
        int cnt = 0;
        boolean[] isPrime = new boolean[n];
        Arrays.fill(isPrime, true);
        isPrime[0] = isPrime[1] = false;
        for(int i = 2; i * i < n; i++){
            if(isPrime[i]){
                for(int j = i * i; j < n; j += i){
                    isPrime[j] = false;
                }
            }
        }
        for(boolean ele: isPrime){
            if(ele){
                cnt++;
            }
        }
        return cnt;
    }
}


# 41. First Missing Positive
# Solution_Link : https://leetcode.com/problems/first-missing-positive/submissions/1885932716

# Code:

class Solution {
    public int firstMissingPositive(int[] nums) {
        int target = 1;
        Arrays.sort(nums);
        for(int i = 0; i < nums.length; i++){
            if(nums[i] > 0 && nums[i] == target){
                target++;
            }
            else if(nums[i] > target){
                return target;
            }
        }
        return target;
    }
}

# 4. Median of Two Sorted Arrays
# Solution_Link : https://leetcode.com/problems/median-of-two-sorted-arrays/submissions/1892929618

# Code :

class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int i = 0;
        int j = 0;
        int m1 = 0;
        int m2 = 0;
        int n1 = nums1.length;
        int n2 = nums2.length;
        for(int cnt = 0; cnt <= (n1 + n2) / 2; cnt++){
            m2 = m1;
            if(i != n1 && j != n2){
                if(nums1[i] > nums2[j]){
                    m1 = nums2[j++];
                }
                else{
                    m1 = nums1[i++];
                }
            } else if(i < n1){
                m1 = nums1[i++];
            }
            else{
                m1 = nums2[j++];
            }
        }
        double ans = 0;
        if((n1 + n2) % 2 == 1){
            return (double) m1;
        }
        else{
            ans = (double) m1 + (double) m2;
        }
        return ans / 2.0;
    }
}

# Weekly Challenges:

# 455. Assign Cookies
# Solution_Link : https://leetcode.com/problems/assign-cookies/submissions/1647090207

# Code:

class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);
        int l = 0;
        int r = 0;
        while(r < g.length && l < s.length){
            if(g[r] <= s[l]){
                r = r + 1;
            }
            l = l + 1;
        }
        return r;
    }
}

# 575. Distribute Candies
# Solution_Link: https://leetcode.com/problems/distribute-candies/submissions/1892960668

# Code:

class Solution {
    public int distributeCandies(int[] candyType) {
        HashSet<Integer> set = new HashSet<>();
        for(int i: candyType){
            set.add(i);
        }
        int n = candyType.length;
        if(set.size() >= (n / 2)) return n/2;
        return set.size(); 
    }
}

# 992. Subarrays with K Different Integers
# Solution_Link : https://leetcode.com/problems/distribute-candies/submissions/1892960668

# Code:

class Solution {
    public int distributeCandies(int[] candyType) {
        HashSet<Integer> set = new HashSet<>();
        for(int i: candyType){
            set.add(i);
        }
        int n = candyType.length;
        if(set.size() >= (n / 2)) return n/2;
        return set.size(); 
    }
}
