# Recursion Problems

## Q1) Dynamic Steps

**Problem :** You are given a number n representing the number of stairs in a staircase. You are standing at the bottom of the staircase. You are allowed to climb either 1 step, 2 steps, or 3 steps in one move. Write a function to print all the possible paths that can be used to climb the staircase.

**Input:** The only line of the input contains a single integer n, representing the number of steps.

**Output:** Print all the stair paths in different lines.

**Approach:** Use recursion to explore all possible paths to climb the stairs.

```
#include <bits/stdc++.h>
using namespace std;

void solve(int n, string curr){
    if(n<=0){
        if(n==0){
            cout << curr << endl;
        }
        return;
    }

    solve(n-1, curr + "1 ");
    solve(n-2, curr + "2 ");
    solve(n-3, curr + "3 ");
}

int main() {
    int n;
    cin >> n;
    solve(n, "");
    return 0;
}
```

**Time Complexity:** O(3^n)
Here, in the worst case, we are making 3 recursive calls for each step until we reach the base case. This leads to an exponential growth in the number of calls, resulting in a time complexity of O(3^n).

**Space Complexity:** O(n)

---

## Q2) Sort a Stack using Recursion

**Problem:** Sort a stack using recursion.

**Approach:** Use recursion to sort the stack by popping all elements and inserting them in sorted order.

```
class Solution {
  public:

    void insertAtBottom(stack<int> &st, int num){
    if(st.empty() || st.top() <= num){
        st.push(num);
        return;
    }

    int top = st.top();
    st.pop();

    insertAtBottom(st, num);

    st.push(top);
    }

    void sortStack(stack<int> &st) {
        if(st.empty()){
            return;
        }

        int top = st.top();
        st.pop();

        sortStack(st);

        insertAtBottom(st,top);
    }
};
```

**Time Complexity:** O(n^2)
How is it O(n^2)?

- The `sortStack` function is called n times (once for each element in the stack).
- Each time `insertAtBottom` is called, it may need to traverse the entire stack to insert the element in sorted order, which takes O(n) time in the worst case.

**Space Complexity:** O(n) (due to recursion stack)

---

## Q3) Print all Subsequences of a String

**Problem:** Given a string, print all its possible subsequences.

**Approach:** Use recursion to explore all possible subsequences by **including or excluding** each character.

```
class Solution {
    public:
    void solve(string str, int i, string output, vector<string> &ans){
        // base case
        if (i == str.length()) {
            // if told not to include empty string
            // if (!output.empty()) ans.push_back(output);

            ans.push_back(output);
            return;
        }

        // 1 case
        char ch = str[i];
        // include
        solve(str, i+1, output + ch,ans);
        // exclude
        solve(str,i+1,output,ans);
    }

    vector<string> subsequences(string str) {
        int i = 0;
        vector<string> ans;
        string output = "";
        solve(str,i,output,ans);
        return ans;
    }
};
```

**Time Complexity:** O(2^n)
How is it O(2^n)?
- For each character in the string, we have two choices: include it in the subsequence or exclude it. This leads to a binary tree of choices, resulting in 2^n possible subsequences for a string of length n.

**Space Complexity:** O(n) (due to recursion stack)

---

## Q4) House Robber

**Problem:** You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected, and it will automatically contact the police if two adjacent houses were broken into on the same night. Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

**Approach:** Use recursion to explore all possible combinations of houses to rob.
Using include-exclude approach.

```
class Solution {
public:
    int solve(vector<int>& nums, int i){
        if(i >= nums.size()){
            return 0;
        }

        //include
        int include = nums[i] + solve(nums,i+2);
        //exclude
        int exclude = 0 + solve(nums,i+1);

        return max(include,exclude);
    }

    int rob(vector<int>& nums) {
        int i = 0;
        return solve(nums,i);
    }
}; 
```

**Time Complexity:** O(2^n)
How is it O(2^n)?

- For each house, we have two choices: rob it or not rob it. This leads to a binary tree of choices, resulting in 2^n possible combinations of houses to rob.

**Space Complexity:** O(n) (due to recursion stack)

---