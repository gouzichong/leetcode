# Leetcode 142
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
            ListNode *slow, *fast;
            slow = head;
            fast = head;

            while(fast && fast->next){
                slow = slow->next;
                fast = fast->next->next;
                if(slow == fast){
                    break;
                }
            }

            if(fast == NULL || fast->next == NULL){
                return NULL;
            }        

            ListNode *ret = head;
            while(ret != fast){
                ret = ret->next;
                fast = fast->next;
            }

            return ret;
        }
    };
