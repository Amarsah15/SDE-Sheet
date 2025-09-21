# LinkedList and Arrays Problems

## Q1) Palindrome Linked List

**Problem:** Given the head of a singly linked list, return true if it is a palindrome.

**Naive Approach:** Use stack to store the values of the nodes and then compare.

```
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        stack<int> st;
        ListNode* tail = head;

        while(tail != NULL){
            st.push(tail->val);
            tail = tail->next;
        }

        while(!st.empty()){
            if(head->val != st.top()){
                return false;
            }
            st.pop();
            head = head->next;
        }

        return true;

    }
};

```

**Time Complexity:** O(n)
**Space Complexity:** O(n)

**Optimal Approach:**

**Approach:** Find the middle of the linked list, reverse the second half, and compare it with the first half.

```

class Solution {
public:
    ListNode* reverseList(ListNode* head){
        ListNode* prev = NULL;
        ListNode* pres = head;

        while(pres != NULL){
            ListNode* future = pres->next;
            pres->next = prev;
            prev = pres;
            pres = future;
        }
        return prev;
    }
    bool isPalindrome(ListNode* head) {
        ListNode* fast = head;
        ListNode* slow = head;

        while(fast->next != NULL && fast->next->next != NULL){
            slow = slow->next;
            fast = fast->next->next;
        }

        slow->next = reverseList(slow->next);
        slow = slow->next;

        while(slow != NULL){
            if(head->val != slow->val){
                return false;
            }
            head = head->next;
            slow = slow->next;
        }

        return true;
    }
};

```

**Time Complexity:** O(n)
**Space Complexity:** O(1)

---

## Q2) Linked List Cycle II

**Problem:** Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return null.

**Approach:** Use Floyd's Cycle-Finding Algorithm to detect a cycle in the linked list.

```

class Solution {
public:
    ListNode *detectCycle(ListNode *head) {

        if(head == NULL || head->next == NULL) return NULL;

        ListNode* fast = head;
        ListNode* slow = head;

        while(fast->next != NULL && fast->next->next != NULL){
            fast = fast->next->next;
            slow = slow->next;

            if(slow == fast){
                fast = head;
                while(fast != slow){
                    fast = fast->next;
                    slow = slow->next;
                }
                return fast;
            }
        }

        return NULL;
    }
};

```

**Time Complexity:** O(n)
**Space Complexity:** O(1)

---

## Q3) Reverse Nodes in k-Group

**Problem:** Given the head of a linked list, reverse the nodes of the list k at a time and return the modified list.

**Approach:** Iterate through the list in groups of k nodes and reverse each group.

```
class Solution {
public:
    ListNode* reverseLinkedList(ListNode* head) {
        ListNode* curr = head;
        ListNode* prev = NULL;

        while (curr != NULL) {
            ListNode* front = curr->next;
            curr->next = prev;
            prev = curr;
            curr = front;
        }

        return prev;
    }

    ListNode* getKthNode(ListNode* temp, int k) {
        k -= 1;

        while (temp != NULL && k > 0) {
            k--;
            temp = temp->next;
        }

        return temp;
    }

    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode* temp = head;
        ListNode* prevLast = NULL;

        while (temp != NULL) {
            ListNode* kThNode = getKthNode(temp, k);

            if (kThNode == NULL) {
                if (prevLast) {
                    prevLast->next = temp;
                }
                break;
            }

            ListNode* nextNode = kThNode->next;
            kThNode->next = NULL;

            reverseLinkedList(temp);

            if (temp == head) {
                head = kThNode;
            } else {
                prevLast->next = kThNode;
            }

            prevLast = temp;
            temp = nextNode;
        }

        return head;
    }
};

```

**Time Complexity:** O(n)
**Space Complexity:** O(1)

**Approach:** Recursively reverse k nodes at a time.

```

class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        // recursively
        ListNode* temp = head;
        int count = 0;

        // temp ko end takh lekar jao
        while(count < k){
            count++;
            if(temp == NULL) return head;
            temp = temp->next;
        }

        // recusively temp takh saaara node reverse hogaya h
        ListNode* prevNode = reverseKGroup(temp,k);

        // phele k Ktj node ko reverse kardo manually
        temp = head;
        count = 0;

        while(count < k){
            ListNode* next = temp->next;
            temp->next = prevNode;

            prevNode = temp;
            temp = next;

            count++;
        }

        return prevNode;
    }
};

```

**Time Complexity:** O(n)
**Space Complexity:** O(n) (due to recursion stack) -> O(n/k) due to recursion stack\*\* 👉 In the worst case (k = 1), recursion depth = n`, so O(n).

Recursion stack:

• Each recursive call processes k nodes and then calls again for the rest.
• In the worst case, we have n/k recursive calls.

---

## Q4) Max Consecutive Ones

**Problem:** Given a binary array, find the maximum number of consecutive 1s in this array.

**Approach:** Iterate through the array and count consecutive 1s, updating the maximum count when a 0 is encountered.

```

class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int count = 0;
        int ans = 0;

        for(int i=0;i<nums.size();i++){
            if(nums[i] == 1){
                count++;
                ans = max(ans,count);
            }
            else{
                count = 0;
            }
        }

        return ans;
    }
};

```

**Time Complexity:** O(n)
**Space Complexity:** O(1)

---
