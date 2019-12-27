# Leetcode 19
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
        ListNode* removeNthFromEnd(ListNode* head, int n) {
            ListNode *next = head;      
            while(n){
                next = next->next;
                n--;
            }

            if(next == NULL){
                return head->next;
            } 

            ListNode *pre = head; 
            while(next){
                next = next->next;
                if(next == NULL){
                    break;
                }
                pre = pre->next;
            }

            pre->next = pre->next->next;

            return head;
        }
    };
