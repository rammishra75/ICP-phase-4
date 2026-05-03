# Letter Combination of  a phone number:

```
class Solution {
    public List<String> letterCombinations(String digits) {
        if(digits.length() == 0)  return new ArrayList<>();
        List<String> ans = new ArrayList<>();
        HashMap<Integer, String> mpp = new HashMap<>();
        mpp.put(2, "abc");
        mpp.put(3, "def");
        mpp.put(4, "ghi");
        mpp.put(5, "jkl");
        mpp.put(6, "mno");
        mpp.put(7, "pqrs");
        mpp.put(8, "tuv");
        mpp.put(9, "wxyz");
        backtrack(digits, 0, mpp, ans, new StringBuilder());
        return ans;
    }
    public void backtrack(String dig, int i, HashMap<Integer, String> mpp, List<String> list, StringBuilder s){
        if(i == dig.length()){
            list.add(s.toString());
            return;
        }
        String letters = mpp.get(dig.charAt(i) - '0');
        for(char l : letters.toCharArray()){
            s.append(l);
            backtrack(dig, i + 1, mpp, list, s);
            s.deleteCharAt(s.length() - 1);
        }
    }
}
```
