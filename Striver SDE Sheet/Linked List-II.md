# Linked List II

## Find the intersection point of Y LL

- [LeetCode](https://leetcode.com/problems/intersection-of-two-linked-lists/)

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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* ptr1 = headA;
        ListNode* ptr2 = headB;
        int cnt = 0;
        while(cnt < 3) {
            if(ptr1 == ptr2) {
                return ptr1;
            } else {
                if(ptr1->next == nullptr){
                    ptr1 = headB;
                    cnt++;
                } else {
                    ptr1 = ptr1->next;
                }

                if(ptr2->next == nullptr){
                    ptr2 = headA;
                    cnt++;
                } else {
                    ptr2 = ptr2->next;
                }
            }
        }

        return nullptr;
    }
};
```

## Detect Loop in LL

- [LeetCode](https://leetcode.com/problems/linked-list-cycle/)

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
    bool hasCycle(ListNode *head) {
        ListNode* slow = head;
        ListNode* fast = head;

        while(fast != nullptr && fast->next != nullptr) {
            fast = fast->next->next;
            slow = slow->next;

            if(fast == slow) return true;
        }

        return false;
    }
};
```

## Reverse LL in groups of given size K

- [LeetCode](https://leetcode.com/problems/reverse-nodes-in-k-group)

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
    ListNode* getKthNode(ListNode* curr, int k) {
        while (curr && k > 0) {
            curr = curr->next;
            k--;
        }
        return curr;
    }

    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode* dummy = new ListNode(0, head);

        ListNode* groupPrev = dummy;

        while (true) {
            ListNode* kth = getKthNode(groupPrev, k);
            if (!kth)
                break;

            ListNode* groupNext = kth->next;


            ListNode* prev = groupNext;
            ListNode* curr = groupPrev->next;

            for (int i = 0; i < k; i++) {
                ListNode* temp = curr->next;
                curr->next = prev;
                prev = curr;
                curr = temp;
            }

            ListNode* temp = groupPrev->next;
            groupPrev->next = kth;
            groupPrev = temp;
        }

        return dummy->next;
    }
};
```

## Check if LL is Palindrome or not

- [LeetCode](https://leetcode.com/problems/palindrome-linked-list/)

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
    bool isPalindrome(ListNode* head) {
        ListNode* slow = head;
        ListNode* fast = head;


        while(fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
        }

        ListNode* prev = nullptr;
        ListNode* curr = slow;

        while(curr != nullptr) {
            ListNode* next = curr->next;

            curr->next = prev;
            prev = curr;
            curr = next;
        }

        fast = prev;

        while(head != nullptr && fast != nullptr) {
            if(head->val != fast->val) {
                return false;
            }

            head = head->next;
            fast = fast->next;
        }

        return true;
    }
};
```

## Find the starting point of Loop in LL

- [LeetCode](https://leetcode.com/problems/linked-list-cycle-ii/)

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
    ListNode *detectCycle(ListNode *head) {
        if(!head || !head->next) {
            return nullptr;
        }

        ListNode* slow = head;
        ListNode* fast = head;

        while(fast != nullptr && fast->next != nullptr) {
            fast = fast->next->next;
            slow = slow->next;

            if(fast == slow) break;
        }

        if(fast != slow) return nullptr;

        while(head != slow) {
            head = head->next;
            slow = slow->next;
        }

        return slow;
    }
};
```
