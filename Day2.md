# LinkedList Problems

## Q1) Add Two Numbers

**Problem:** You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

**Approach:** Iterative solution that adds digits and handles carryover.

```

class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* dummy = new ListNode(0);
        ListNode* curr = dummy;
        int digit = 0;

        while (l1 != NULL || l2 != NULL || digit != 0) {
            int sum = digit;
            if (l1 != NULL) {
                sum += l1->val;
                l1 = l1->next;
            }
            if (l2 != NULL) {
                sum += l2->val;
                l2 = l2->next;
            }

            digit = sum / 10;
            curr->next = new ListNode(sum % 10);
            curr = curr->next;
        }

        return dummy->next;
    }
};

```

**Time Complexity:** O(max(m, n)) where m and n are the lengths of the two lists
**Space Complexity:** This is O(max(m, n)), but since this is the required output, we don’t usually count it as extra space. So, the auxiliary space is O(1).

## Q2) Delete Node in a Linked List

**Problem:** Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

**Approach:** Copy the value from the next node to the current node and delete the next node.

```

class Solution {
public:
    void deleteNode(ListNode* node) {
        node->val = node->next->val;
        node->next = node->next->next;
    }
};

```

**Time Complexity:** O(1)
**Space Complexity:** O(1)

## Q3) Intersection of Two Linked Lists

**Problem:** Given the heads of two singly linked-lists headA and headB, return the node at which the two lists intersect. If the two linked lists have no intersection at all, return null.

**Approach:** Iterative solution that uses two pointers to find the intersection.

```

class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if (!headA || !headB) return NULL;

        ListNode* d1 = headA;
        ListNode* d2 = headB;

        while (d1 != d2) {
            d1 = (d1 == NULL) ? headB : d1->next;
            d2 = (d2 == NULL) ? headA : d2->next;
        }

        return d1;
    }
};

```

**Time Complexity:** O(m + n)
**Space Complexity:** O(1)

## Q4) Linked List Cycle

**Problem:** Given a linked list, determine if it has a cycle in it.

**Approach:** Floyd's Cycle-Finding Algorithm

```

class Solution {
public:
    bool hasCycle(ListNode* head) {
        if(head == NULL || head->next == NULL){
            return false;
        }

        ListNode* fast = head;
        ListNode* slow = head;

        while(fast != NULL && fast->next != NULL){
            fast = fast->next->next;
            slow = slow->next;

            if(slow == fast){
                return true;
            }
        }

        return false;
    }
};

```

**Time Complexity:** O(n)
**Space Complexity:** O(1)
