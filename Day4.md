# Recursion Problems

## Q1) Fibonacci Number

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

---

## Q2) Climbing Stairs

**Problem:** You are climbing a staircase. It takes n steps to reach the top. Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Approach:** Simple recursion to calculate number of ways to climb stairs.

But what recursion relation is this problem following?

We assume that we are at step 'i'. Now, we can reach step 'i' from either step 'i-1' or step 'i-2'. So, the total number of ways to reach step 'i' is the sum of the number of ways to reach steps 'i-1' and 'i-2'.
How we think of base cases?

- If we are at step 0, there is only 1 way to stay there (do nothing).
- If we are at step 1, there is only 1 way to reach there (take a single step).

Now, we have to find the number of ways to reach steps 'i-1' and 'i-2'. We can do that by calling the function recursively.

```
class Solution {
public:
    int climbStairs(int n) {
        if(n == 0){
            return 1;
        }

        if(n == 1){
            return 1;
        }


        return climbStairs(n-1) + climbStairs(n-2);
    }
};
```

**Time Complexity:** O(2^n)
**Space Complexity:** O(n) (due to recursion stack)

---
