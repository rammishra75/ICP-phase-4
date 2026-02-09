# Assignment : 4

# 1290. Convert a Binary Number in a Linked List to an Integer
# Solution Link : https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer/submissions/1906571630

# Code:
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public int getDecimalValue(ListNode head) {
        ListNode curr = head;
        int num = 0;
        while(curr != null){
            num = (num << 1) | curr.val;
            curr = curr.next;
        }
       
     
        return num;
    }
}
```

# 2095. Delete the Middle Node of a Linked List
# Solution Link : https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/submissions/1905370636
# Code:
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode deleteMiddle(ListNode head) {
        if(head == null || head.next == null){
            return null;
        }
        ListNode slow = head;
        ListNode fast = head;
        fast = head.next.next;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        slow.next = slow.next.next;
        return head;
    }
}
```

# 3510. Minimum Pair Removal to Sort Array II
# Solution Link:  https://leetcode.com/problems/minimum-pair-removal-to-sort-array-ii/submissions/1913405407
# Code:
```
class Solution {

    static class Pair {
        long sum;
        int idx;

        Pair(long sum, int idx) {
            this.sum = sum;
            this.idx = idx;
        }

        @Override
        public boolean equals(Object o) {
            if (this == o) return true;
            if (!(o instanceof Pair)) return false;
            Pair p = (Pair) o;
            return sum == p.sum && idx == p.idx;
        }

        @Override
        public int hashCode() {
            return Objects.hash(sum, idx);
        }
    }

    public int minimumPairRemoval(int[] nums) {
        int n = nums.length;

        // {a, b, c, d} -> {a, b+c, d}
        long[] temp = new long[n];
        for (int i = 0; i < n; i++) {
            temp[i] = nums[i];
        }

        TreeSet<Pair> minPairSet = new TreeSet<>(
            (a, b) -> {
                if (a.sum != b.sum) return Long.compare(a.sum, b.sum);
                return Integer.compare(a.idx, b.idx);
            }
        );

        int[] nextIndex = new int[n];
        int[] prevIndex = new int[n];

        for (int i = 0; i < n; i++) {
            nextIndex[i] = i + 1;
            prevIndex[i] = i - 1;
        }

        int badPairs = 0;
        for (int i = 0; i < n - 1; i++) {
            if (temp[i] > temp[i + 1]) {
                badPairs++;
            }
            minPairSet.add(new Pair(temp[i] + temp[i + 1], i));
        }

        int operations = 0;

        while (badPairs > 0) {

            Pair cur = minPairSet.first();
            minPairSet.remove(cur);

            int first = cur.idx;
            int second = nextIndex[first];

            int first_left = prevIndex[first];
            int second_right = nextIndex[second];

            if (temp[first] > temp[second]) {
                badPairs--;
            }

            // {d, (a, b)}
            if (first_left >= 0) {
                if (temp[first_left] > temp[first] &&
                    temp[first_left] <= temp[first] + temp[second]) {
                    badPairs--;
                }
                else if (temp[first_left] <= temp[first] &&
                         temp[first_left] > temp[first] + temp[second]) {
                    badPairs++;
                }
            }

            // {(a, b), d}
            if (second_right < n) {
                if (temp[second_right] >= temp[second] &&
                    temp[second_right] < temp[first] + temp[second]) {
                    badPairs++;
                }
                else if (temp[second_right] < temp[second] &&
                         temp[second_right] >= temp[first] + temp[second]) {
                    badPairs--;
                }
            }

            if (first_left >= 0) {
                minPairSet.remove(
                    new Pair(temp[first_left] + temp[first], first_left)
                );
                minPairSet.add(
                    new Pair(temp[first_left] + temp[first] + temp[second], first_left)
                );
            }

            if (second_right < n) {
                minPairSet.remove(
                    new Pair(temp[second] + temp[second_right], second)
                );
                minPairSet.add(
                    new Pair(temp[first] + temp[second] + temp[second_right], first)
                );
                prevIndex[second_right] = first;
            }

            nextIndex[first] = second_right;
            temp[first] += temp[second];

            operations++;
        }

        return operations;
    }
}
```

# 4)2816. Double a Number Represented as a Linked List 
# Solution Link: https://leetcode.com/problems/double-a-number-represented-as-a-linked-list/submissions/1906622465
# Code:
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
 class Solution {
    public ListNode doubleIt(ListNode head) {
        Stack<ListNode> stk = new Stack<>();
        ListNode curr = head;

        while (curr != null) {
            stk.push(curr);
            curr = curr.next;
        }

        int carry = 0;

        while (!stk.isEmpty()) {
            curr = stk.pop();
            int val = curr.val * 2 + carry;
            curr.val = val % 10;
            carry = val / 10;
        }

        if (carry > 0) {
            ListNode newHead = new ListNode(carry);
            newHead.next = head;
            head = newHead;
        }

        return head;
    }
}
```

# 2289 Steps to Make Array Non-decreasing  
# Solution Link: https://leetcode.com/problems/steps-to-make-array-non-decreasing/submissions/1910376036
# Code:
```
class Solution {
    public int totalSteps(int[] nums) {
       int n = nums.length;
       int ans = 0;
       Stack<Pair<Integer, Integer>> stk = new Stack<>();
       stk.push(new Pair<>(nums[n - 1], 0));
       for(int i = n - 2; i >= 0; i--){
            int cnt = 0;
            while(!stk.isEmpty() && nums[i] > stk.peek().getKey()){
                cnt = Math.max(cnt + 1, stk.peek().getValue());
                stk.pop();
            }
            ans = Math.max(ans, cnt);
            stk.push(new Pair(nums[i], cnt));
       }
       return ans;
    }
}
```

#6)1019. Next Greater Node In Linked List          
# Solution Link : https://leetcode.com/problems/next-greater-node-in-linked-list/submissions/1907614066
# Code:
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public int[] nextLargerNodes(ListNode head) {
        ListNode curr = head;
        ArrayList<Integer> list = new ArrayList<>();
        Stack<Integer> stk = new Stack<>();
        while(curr != null){
            list.add(curr.val);
            curr = curr.next;
        }
        int len = list.size();
        int[] ans = new int[len];
        for(int i = len - 1; i >= 0; i--){
            int ele = list.get(i);
            while(!stk.isEmpty() && stk.peek() <= ele){
                stk.pop();
            }
            if(stk.isEmpty()) ans[i] = 0;
            else ans[i] = stk.peek();
            stk.push(ele);
        }
        return ans;
    }
}
```
