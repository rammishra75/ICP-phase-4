# Largest rectangle in Histogram

```
class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length;
        int maxArea = 0;
        Stack<Integer> st = new Stack<>();
        for(int i = 0 ; i < n; i++){
            while(!st.isEmpty() && heights[st.peek()] >= heights[i]){
                int height = heights[st.peek()];
                st.pop();
                int nse = i;
                int pse = st.isEmpty() ? -1 : st.peek();
                int width = nse - pse - 1;
                maxArea = Math.max(maxArea, width * height);
            }
            st.push(i);
        }
        while(!st.isEmpty()){
            int nse = n;
            int height = heights[st.peek()];
            st.pop();
            int pse = st.isEmpty()?-1 : st.peek();
            int width = nse - pse - 1;
            maxArea = Math.max(maxArea, height * width);
        }
        return maxArea;
    }
}
```
