# N- Queens Backtracking

```
class Solution {
    public void solve(int col, char[][] board, List<List<String>> ans, int[] leftRow, int[] upperD, int[] lowerD){
        if(col == board.length){
            ans.add(construct(board));
            return;
        }

        for(int row = 0; row < board.length; row++){
            if(leftRow[row] == 0 && lowerD[row + col] == 0 && upperD[board.length - 1 + col - row] == 0){
                board[row][col] = 'Q';
                leftRow[row] = 1;
                upperD[board.length - 1 + col - row] = 1;
                lowerD[row + col] = 1;
                solve(col + 1, board, ans, leftRow, upperD, lowerD);
                board[row][col] = '.';
                leftRow[row] = 0;
                upperD[board.length - 1 + col - row] = 0;
                lowerD[row + col] = 0;
            }
        }
    }
    public List<String> construct(char[][] board){
        List<String> res = new LinkedList< String >();
        for(int i = 0; i < board.length; i++){
            String s = new String(board[i]);
            res.add(s);
        }
        return res;
    }
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> ans = new ArrayList<>();
        char[][] board = new char[n][n];
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                board[i][j] = '.';
            }
        }
        int[] leftRow = new int[n];
        int[] upperDiagonal = new int[2 * n - 1];
        int[] lowerDiagonal = new int[2 * n - 1];
        solve(0, board, ans, leftRow, upperDiagonal, lowerDiagonal);
        return ans;
    }
}
```
