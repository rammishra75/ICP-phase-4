# Week - 6 Assignment

# 1325. Delete Leaves With a Given Value
# Solution Link : https://leetcode.com/problems/delete-leaves-with-a-given-value/submissions/1920756378

# Solution code:
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode removeLeafNodes(TreeNode root, int target) {
        if(root == null) return root;
        root.left = removeLeafNodes(root.left, target);
        root.right = removeLeafNodes(root.right, target);
        if(root.left == null && root.right == null && root.val == target) return null;
        return root;
    }
}
```



# 2476. Closest Nodes Queries in a Binary Search Tree
# Solution Link : https://leetcode.com/problems/closest-nodes-queries-in-a-binary-search-tree/submissions/1922990250
# Solution code: 
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int findmin(int num, List<Integer> arr){
        int ans = -1;
        int low = 0;
        int high = arr.size() - 1;
        while(low <= high){
            int mid = low + (high - low) / 2;
            if(arr.get(mid) >= num){
                ans = arr.get(mid);
                high = mid - 1;
            }
            else{
                low = mid + 1;
            }
        }
        //if(ans == Integer.MIN_VALUE) return -1;
        return ans;
    }
    public int findmax(int num, List<Integer> arr){
        int ans = -1;
        int low = 0;
        int high = arr.size() - 1;
        while(low <= high){
            int mid = low + (high - low) / 2;
            if(arr.get(mid) <= num){
                ans = arr.get(mid);
                low = mid + 1;
            }
            else{
                high = mid - 1;
            }
        }
        return ans;
    }
    public void traverse(TreeNode root, List<Integer> arr){
        if(root == null) return;
        traverse(root.left, arr);
        arr.add(root.val);
        traverse(root.right, arr);
    }
    public List<List<Integer>> closestNodes(TreeNode root, List<Integer> queries) {
        List<List<Integer>> ans = new ArrayList<>();
        List<Integer> arr = new ArrayList<>();
        traverse(root, arr);
        for(int i : queries){
            int max = findmin(i, arr);
            int min = findmax(i, arr);
            List<Integer> temp = new ArrayList<>();
            temp.add(min);
            temp.add(max);
            ans.add(temp);
        }
        return ans;
    }
}
```

# 3)Segment Tree -query of sum-II
# Solution Link : Its on gfg
# Solution Code:
```
class Solution {
    List<Integer> querySum(int n, int arr[], int q, int queries[]) {
        // code here
        int[] pref = new int[n];
        for(int i = 0; i < n; i++){
            pref[i] = arr[i];
            if(i > 0) pref[i] += pref[i - 1];
        }
        List<Integer> ans = new ArrayList<>();
        int i = 0;
        while(i < (2 * q)){
            int strt = queries[i] - 1;
            int end = queries[i + 1] - 1;
            int sum = pref[end];
            if(strt - 1 >= 0) sum -= pref[strt - 1];
            ans.add(sum);
            i += 2;
        }
        return ans;
    }
}
```


# 1382. Balance a Binary Search Tree
# Solution Link : https://leetcode.com/problems/balance-a-binary-search-tree/submissions/1922885604

# Solution Code:
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode buildTree(int left, int right, List<Integer> arr){
        if(left > right) return null;
        int mid = left + (right - left) / 2;
        TreeNode root = new TreeNode(arr.get(mid));
        root.left = buildTree(left, mid - 1, arr);
        root.right = buildTree(mid + 1, right, arr);
        return root;
    }
    public void traverse(TreeNode root, List<Integer> arr){
        if(root == null) return;
        traverse(root.left, arr);
        arr.add(root.val);
        traverse(root.right, arr);
    }
    public TreeNode balanceBST(TreeNode root) {
        List<Integer> arr = new ArrayList<>(); 
        traverse(root, arr);
        return buildTree(0, arr.size() - 1, arr);
    }
}
```

# 1932. Merge BSTs to Create Single BST
# Solution Link: https://leetcode.com/problems/merge-bsts-to-create-single-bst/submissions/1922951301
# Code:

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    Map<Integer, TreeNode> mpp = new HashMap<>();
    Set<Integer> leaves = new HashSet<>();

    public TreeNode canMerge(List<TreeNode> trees) {
        for(TreeNode tree: trees){
            mpp.put(tree.val, tree);
            if(tree.left != null) leaves.add(tree.left.val);
            if(tree.right != null) leaves.add(tree.right.val);
        }

        TreeNode root = null;
        for(TreeNode node: trees){
            if(!leaves.contains(node.val)){
                root = node;
                break;
            }
        }
        if(root == null) return null;

        mpp.remove(root.val);

        if(!validateAndMergeBST(root, Long.MIN_VALUE, Long.MAX_VALUE)) return null;
        if(!mpp.isEmpty()) return null;

        return root;
    }

    private boolean validateAndMergeBST(TreeNode node, long minVal, long maxVal){
        if(node == null) return true;

        if(node.val <= minVal || node.val >= maxVal){
            return false;
        }

        if(node.left != null && mpp.containsKey(node.left.val)){
            node.left = mpp.get(node.left.val);
            mpp.remove(node.left.val);
        }

        if(node.right != null && mpp.containsKey(node.right.val)){

            node.right = mpp.get(node.right.val);
            mpp.remove(node.right.val);
        }

        return validateAndMergeBST(node.left, minVal, node.val) && validateAndMergeBST(node.right, node.val, maxVal);
    }
}
```

# 2673. Make Costs of Paths Equal in a Binary Tree
# Solution Link : https://leetcode.com/problems/make-costs-of-paths-equal-in-a-binary-tree/submissions/1922977272
# Code:

```
class Solution {
    int ans = 0;
    public int dfs(int n, int[] cost, int i){
        if(i > n) return 0;
        int leftCost = dfs(n, cost, 2 * i);
        int rightCost = dfs(n, cost, 2 * i + 1);
        ans += Math.abs(leftCost - rightCost);
        return Math.max(leftCost, rightCost) + cost[i - 1];
    }
    public int minIncrements(int n, int[] cost) {
        dfs(n, cost, 1);
        return ans;
    }
}
```

