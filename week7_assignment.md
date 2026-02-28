# Week 7 Assignment

# Depth Search 
# Word Search Problem

# Solution Link : https://leetcode.com/problems/word-search/submissions/1886544764
# Code:
```
class Solution {
    public boolean func(int row, int col, char[][] board, int[][] vis, String word, int ind, int[] drow, int[] dcol){
        if(ind == word.length() ){
            return true;
        }
        if(row < 0 || row >= board.length || col < 0 || col >= board[0].length || vis[row][col] == 1 || board[row][col] != word.charAt(ind)){
            return false;
        }
        vis[row][col] = 1;
        for(int i = 0; i < 4; i++){
            int nrow = row + drow[i];
            int ncol = col + dcol[i];
            if(func(nrow, ncol, board, vis, word, ind + 1, drow, dcol)) return true;
        }
        vis[row][col] = 0;
        return false;
    }
    public boolean exist(char[][] board, String word) {
        int n = board.length;
        int m = board[0].length;
        int[][] vis = new int[n][m];
        int[] drow = {-1, 0, 1, 0};
        int[] dcol = {0, 1, 0, -1};
       
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(board[i][j] == word.charAt(0)){
                    if(func(i, j, board, vis, word,0, drow, dcol)) return true;
                   
                }
            }
        }
        return false;
    }
}

```

# Number of Islands:
# Solution Link: https://leetcode.com/problems/number-of-islands/submissions/1667099125
# Solution COde:
```
class Solution {
    public int numIslands(char[][] grid) {
        int cnt = 0;
        int n = grid.length;
        int m = grid[0].length;
        int[][] vis = new int[n][m];
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(vis[i][j] == 0 && grid[i][j] == '1'){
                    cnt++;
                    dfs(i, j, vis, grid, n, m);
                }
            }
        }
        return cnt;
    }
    public static void dfs(int r, int c, int[][] vis, char[][] grid, int n, int m){
        int[] dr = {-1, 0, 1, 0};
        int[] dc = {0, 1, 0, -1};
        for(int i = 0; i < 4; i++){
            int nr = r + dr[i];
            int nc = c + dc[i];
            if(nr >= 0 && nr < n && nc >= 0 && nc < m && vis[nr][nc] == 0 && grid[nr][nc] == '1'){
                vis[nr][nc] = 1;
                dfs(nr, nc, vis, grid, n , m);
            }
        }
    }
}
```

# Is Graph Bipartite
# Solution Link : https://leetcode.com/problems/is-graph-bipartite/submissions/1679135746
# Solution Code:
```
class Solution {
    public boolean dfs(int node, int color, int[] paint, int[][] graph){
        paint[node] = color;
        for(int it : graph[node]){
            if(paint[it] == -1){
                if(dfs(it, 1 - color, paint, graph) == false){
                    return false;
                }
            }
            else if(paint[it] == color){
                return false;
            }
        }
        return true;
    }
    public boolean isBipartite(int[][] graph) {
        int n = graph.length;
        int[] color = new int[n];
        Arrays.fill(color, -1);
        for(int i = 0; i < n; i++){
            if(color[i] == -1){
                if(dfs(i, 1, color, graph) == false){
                    return false;
                }
            }
        }
        return true;
    }
}
```

# 01 Matrix
# Solution Link : https://leetcode.com/problems/01-matrix/submissions/1671259026
# Code:
```
class Solution {
    class Pair{
        int first;
        int second;
        int third;
        Pair(int first, int second, int third){
            this.first = first;
            this.second = second;
            this.third = third;
        }
    }
    public int[][] updateMatrix(int[][] mat) {
        int n = mat.length;
        int m = mat[0].length;
        int[][] vis = new int[n][m];
        int[][] dis = new int[n][m];
        Queue<Pair> q = new LinkedList<>();
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(mat[i][j] == 0){
                    vis[i][j] = 1;
                    q.add(new Pair(i, j, 0));
                }
                else{
                    vis[i][j] = 0;
                }
            }
        }
        int[] drow = {-1, 0 , 1, 0};
        int[] dcol = {0, 1, 0, -1};
        while(!q.isEmpty()){
            int row = q.peek().first;
            int col = q.peek().second;
            int step = q.peek().third;
            q.remove();
            dis[row][col] = step;
            for(int i = 0; i < 4; i++){
                int nr = row + drow[i];
                int nc = col + dcol[i];
                if(nr >= 0 && nr < n && nc >= 0 && nc < m && vis[nr][nc] == 0){
                    vis[nr][nc] = 1;
                    q.add(new Pair(nr, nc, step + 1));
                }
            }
        }
        return dis;
    }
}
```
