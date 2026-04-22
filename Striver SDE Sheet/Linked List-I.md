# Linked List I

## Reverse a Linked list

- [LeetCode](https://leetcode.com/problems/reverse-linked-list/)

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* prev = NULL;
        ListNode* curr = head;

        while(curr != NULL) {
            ListNode* next = curr->next;

            curr->next = prev;
            prev = curr;
            curr = next;
        }

        return prev;
    }
};
```

## Find Middle of Linked list

- [LeetCode](https://leetcode.com/problems/middle-of-the-linked-list/)

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* slow = head;
        ListNode* fast = head;

        while(fast != NULL && fast->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
        }

        return slow;
    }
};
```

## Merge two sorted lists

- [LeetCode](https://leetcode.com/problems/merge-two-sorted-lists/)

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode* ans = new ListNode();
        ListNode* ptr = ans;

        while (list1 != NULL && list2 != NULL) {
            if (list1->val < list2->val) {
                ptr->next = list1;
                ptr = list1;
                list1 = list1->next;
            } else {
                ptr->next = list2;
                ptr = list2;
                list2 = list2->next;
            }
        }

        while (list1 != NULL) {
            ptr->next = list1;
            ptr = list1;
            list1 = list1->next;
        }
        while (list2 != NULL) {
            ptr->next = list2;
            ptr = list2;
            list2 = list2->next;
        }

        return ans->next;
    }
};
```

## Remove Nth node from the back of LL

- [LeetCode](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* ptr1 = head;
        ListNode* ptr2 = head;

        for (int i = 0; i < n; i++) {
            ptr2 = ptr2->next;
        }

        if(ptr2 == NULL) {
            return head->next;
        }

        while (ptr2->next != NULL) {
            ptr1 = ptr1->next;
            ptr2 = ptr2->next;
        }
        
        ptr1->next = ptr1->next->next;

        return head;
    }
};
```

## Add two numbers as LL

- [LeetCode](https://leetcode.com/problems/add-two-numbers/)

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int digit = 0;
        ListNode* start = nullptr;
        ListNode* currentnode;

        while (l1 != nullptr || l2 != nullptr || digit) {
            if (l1 != nullptr) {
                digit += l1->val;
                l1 = l1->next;
            }

            if (l2 != nullptr) {
                digit += l2->val;
                l2 = l2->next;
            }

            ListNode* next = new ListNode(digit % 10);

            if (start == nullptr) {
                start = next;
                currentnode = start;
            } else {
                currentnode->next = next;
                currentnode = next;
            }
            
            digit /= 10;
        }
        return start;
    }
};
```

## Delete Node in a LL

- [LeetCode](https://leetcode.com/problems/delete-node-in-a-linked-list/)

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    void deleteNode(ListNode* node) {
        while(node != nullptr) {
            node->val = node->next->val;
            
            if(node->next->next == nullptr) {
                node->next = nullptr;
            }

            node = node->next;
        }
    }
};
```
