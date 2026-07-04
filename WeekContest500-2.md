# Sum of Primes between Number and Its Reverse

```
class Solution {
    public boolean isPrime(int n){
        if(n <= 1) return false;
        for(int i = 2; i * i <= n; i++){
            if(n % i == 0) return false;
        }
        return true;
    }
    public int sumOfPrimesInRange(int n) {
        int temp = n;
        int rev = 0;
        while(temp > 0){
            int rem = temp % 10;
            rev = rev * 10 + rem;
            temp /= 10;
        }
        int strt = Math.min(n, rev);
        int end = Math.max(n, rev);
        int sum = 0;
        for(int i = strt; i <= end; i++){
            if(isPrime(i)){
                sum += i;
            }
        }
        return sum;    
    }
}
```
