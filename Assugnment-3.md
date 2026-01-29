# Week - 3 Assignment

# 2073. Time Needed to Buy Tickets
# Solution Link : https://leetcode.com/problems/time-needed-to-buy-tickets/submissions/1898371258

# Code: 
```
class Solution {
    public int timeRequiredToBuy(int[] tickets, int k) {
        int cnt = tickets[k];
        int time = 0;
        Queue<int []> q = new LinkedList<>();
        for(int i = 0; i < tickets.length; i++){
            q.add(new int[]{i, tickets[i]});
        }
        while(cnt != 0){
            time++;
            int[] a = q.remove();
            a[1]--;
            if(a[0] == k) cnt--;
            if(a[1] > 0) q.add(a);
        }
        return time;
    }
}
```

# 1823. Find the Winner of the Circular Game
# Solution Link : https://leetcode.com/problems/find-the-winner-of-the-circular-game/submissions/1898442135

# Code: 
```
class Solution {
    public int findTheWinner(int n, int k) {
        Queue<Integer> q = new LinkedList<>();
        for(int i = 1; i <= n; i++){
            q.add(i);
        }
        while(q.size() != 1){
            for(int i = 1; i < k; i++){
                int ele = q.remove();
                q.add(ele);
            }
            q.remove();
        }
        return q.peek();
    }
}
```

# 3191. Minimum Operations to Make Binary Array Elements Equal to One I
# Solution Link : https://leetcode.com/problems/minimum-operations-to-make-binary-array-elements-equal-to-one-i/submissions/1898509583

# Code: 
```
class Solution {
    public int minOperations(int[] nums) {
        int cnt = 0;
        int n = nums.length;
        for(int i = 0; i <= n - 3; i++){
            if(nums[i] == 0){
                cnt++;
                for(int j = i; j < i + 3; j++){
                    nums[j] ^= 1;
                }
            }
        }
        for(int i = n - 3; i < n; i++){
            if(nums[i] == 0) return -1;
        }
        
        return cnt;
    }
}
```

# 3589. Count Prime-Gap Balanced Subarrays
# Solution Link : https://leetcode.com/problems/count-prime-gap-balanced-subarrays/submissions/1900643294

# Code: 
```
class Solution {
   
    Set<Integer> p=new HashSet<>();
    void sieve(){
        int n=50000;
        boolean []v=new boolean[n+1];
        v[1]=v[0]=true;
        for(int i=2;i*i<=n;i++){
            if(v[i]==false){
                for(int j=i*i;j<=n;j+=i)
                    v[j]=true;
            }
        }
        for(int i=2;i<=n;i++){
            if(v[i]==false)
                p.add(i);
        }
    }

    public int primeSubarray(int[] nums, int k) {
        sieve();
        TreeMap<Integer,Integer> m=new TreeMap<>();
        int cnt,s,res,prev,cur;
        cnt=s=res=0;
        prev=cur=-1;
        for(int i=0;i<nums.length;i++){
            if(p.contains(nums[i])){
                m.put(nums[i],m.getOrDefault(nums[i],0)+1);
                cnt++;
                prev=cur;
                cur=i;
            }
            if(cnt>=2){
                while((m.lastKey()-m.firstKey())>k){
                    if(p.contains(nums[s])){
                        if(m.get(nums[s])==1)
                            m.remove(nums[s]);
                        else
                            m.put(nums[s],m.get(nums[s])-1);
                        cnt--;
                    }
                    s++;
                }
                if(cnt>=2)
                    res+=(prev-s+1);
            }
        }
        return res;
    }
}
```

# 950. Reveal Cards In Increasing Order
# Solution Link : https://leetcode.com/problems/reveal-cards-in-increasing-order/submissions/1843405290

# Code : 
```
class Solution {
    public int[] deckRevealedIncreasing(int[] deck) {
        int n = deck.length;
        Queue<Integer> q = new LinkedList<>();
        Arrays.sort(deck);
        for(int i = 0; i < n; i++){
            q.add(i);
        }
        int[] ans = new int[n];
        int i = 0;
        while(!q.isEmpty()){
            int ind = q.remove();
            ans[ind] = deck[i];
            i++;
            if(!q.isEmpty()){
                int skip = q.remove();
                q.add(skip);
            }
        }
        return ans;
    }
}
```

# 1696. Jump Game VI
# Solution Link : https://leetcode.com/problems/jump-game-vi/submissions/1899936224

# Code: 
```
class Solution {
    public int maxResult(int[] nums, int k) {
        int n = nums.length;
        Deque<Pair<Integer, Integer>> dq = new LinkedList<>(){{
            offer(new Pair<>(0, nums[0]));
        }};
        int max = nums[0];
        for(int i = 1; i < n; i++){
            while(!dq.isEmpty() && dq.peekFirst().getKey() < i - k){
                dq.pollFirst();
            }
            max = nums[i] + (dq.isEmpty() ? 0 : dq.peekFirst().getValue());
            while(!dq.isEmpty() && dq.peekLast().getValue() <= max){
                dq.pollLast();
            }
            dq.offerLast(new Pair<>(i, max));
        }
        return max;
    }
}
```
