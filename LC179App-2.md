# Largest Number

# using basic comparator

```
class Solution {
    public String largestNumber(int[] nums) {
        int n = nums.length;
        String[] numStrings = new String[n];
        for(int i = 0; i < n; i++){
            numStrings[i] = Integer.toString(nums[i]);
        }
        Arrays.sort(numStrings, (a, b) -> (b + a).compareTo(a + b));
        if(numStrings[0].equals("0")) return "0";
        StringBuilder largestNum = new StringBuilder();
        for(String num : numStrings){
            largestNum.append(num);
        }
        return largestNum.toString();
    }
}
```
