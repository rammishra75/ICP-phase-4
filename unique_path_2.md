# Unique path with obstacles:

```
import java.util.*;

class Solution {
    private int func(int i, int j, int[][] matrix, int[][] dp) {
        // Base cases
        if (i < 0 || j < 0 || matrix[i][j] == 1) return 0;
        else if (i == 0 && j == 0) return 1;

        // If the result is already computed, return it
        if (dp[i][j] != -1) return dp[i][j];

        /* Calculate the number of ways by
        moving up and left recursively. */
        int up = func(i - 1, j, matrix, dp);
        int left = func(i, j - 1, matrix, dp);

        // Return the total ways
        return dp[i][j] = up + left;
    }

    /* Function to find all unique paths to reach
    matrix[m-1][n-1] from matrix[0][0] with obstacles */
    public int uniquePathsWithObstacles(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;

        // Initialize DP table to memoize results
        int[][] dp = new int[m][n];
        for (int[] row : dp) Arrays.fill(row, -1);

        // Return the total number of paths
        return func(m - 1, n - 1, matrix, dp);
    }
}

class Main {
    public static void main(String[] args) {
        int[][] maze = {
            {0, 0, 0},
            {0, 1, 0},
            {0, 0, 0}
        };

        // Create an instance of Solution class
        Solution sol = new Solution();

        System.out.println("Number of paths with obstacles: " + sol.uniquePathsWithObstacles(maze));
    }
}

```
