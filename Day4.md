# Recursion Problems

### Q1) Fibonacci Number

**Problem:** The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,

F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.

**Approach:** Simple recursion to calculate Fibonacci number.

```
class Solution {
public:
    int solveUsingRecc(int n){
        if(n <= 0){
            return 0;
        }

        if(n == 1){
            return 1;
        }

        int sum = solveUsingRecc(n-1) + solveUsingRecc(n-2);

        return sum;
    }

    int fib(int n) {
        int ans = solveUsingRecc(n);
        return ans;
    }
};
```

**Time Complexity:** O(2^n)
**Space Complexity:** O(n) (due to recursion stack)