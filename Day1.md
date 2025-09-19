# LinkedList Problems

## Q1) Reverse a LinkedList

**Problem:** Reverse a singly linked list.

**Approach:** Iterative solution that reverses the list.

```

class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* prev = nullptr;
        ListNode* curr = head;

        while (curr != nullptr) {
            ListNode* nextNode = curr->next;
            curr->next = prev;
            prev = curr;
            curr = nextNode;
        }

        return prev;
    }
};

```

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

**Approach:** Recursive solution that reverses the list.

```


class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if (head == nullptr || head->next == nullptr)
            return head;

        ListNode* newHead = reverseList(head->next);
        head->next->next = head;
        head->next = nullptr;
        return newHead;
    }
};

```

**Time Complexity:** O(n)  
**Space Complexity:** O(n) due to recursion stack

---

## Q2) Find the Middle of LinkedList

**Problem:** Find the middle node of a linked list. If there are two middle nodes, return the second middle node.

**Approach:** Two-pointer technique (Floyd's tortoise and hare algorithm) where fast pointer moves 2 steps and slow pointer moves 1 step.

```

class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* fast = head;
        ListNode* slow = head;

        while (fast != NULL && fast->next != NULL) {
            fast = fast->next->next;
            slow = slow->next;
        }

        return slow;
    }
};

```

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

---

## Q3) Merge Two Sorted Lists

**Problem:** Merge two sorted linked lists and return it as a sorted list.

**Approach:** Iterative solution that compares values and builds the merged list by adjusting pointers.

```

class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        if (!list1) return list2;
        if (!list2) return list1;

        // Step 1: Decide the head
        ListNode* head = nullptr;
        if (list1->val <= list2->val) {
            head = list1;
            list1 = list1->next;
        } else {
            head = list2;
            list2 = list2->next;
        }

        // Step 2: Use 'tail' to attach next nodes
        ListNode* tail = head;

        while (list1 && list2) {
            if (list1->val <= list2->val) {
                tail->next = list1;
                list1 = list1->next;
            } else {
                tail->next = list2;
                list2 = list2->next;
            }
            tail = tail->next; // move tail forward
        }

        // Step 3: Attach remaining nodes
        if (list1) tail->next = list1;
        if (list2) tail->next = list2;

        return head;
    }
};

```

**Time Complexity:** O(m + n)  
**Space Complexity:** O(1)

---

## Q4) Remove Nth Node From End of List

**Problem:** Remove the nth node from the end of the list and return its head.

**Approach:**

```

class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {

}

```

**Time Complexity:**
**Space Complexity:**

---
