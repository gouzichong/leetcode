# Leetcode 23
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

        ListNode *mergeTwo(ListNode *l1, ListNode *l2){
            ListNode *newNode = new ListNode(0);
            ListNode *head = newNode;
            while(l1 && l2){
                if(l1->val < l2->val){
                    head->next = l1;
                    l1 = l1->next;
                }else{
                    head->next = l2;
                    l2 = l2->next;
                }
                head = head->next;
            }

            head->next = l1 ? l1 : l2;

            return newNode->next;
        }


        /*
        ListNode* mergeKLists(vector<ListNode*>& lists) {
            if(lists.size() == 0){
                return NULL;
            }
            ListNode *ret = lists[0];

            for(int i = 1; i < lists.size(); i++){
                ret = mergeTwo(ret, lists[i]);
            }

            return ret;
        }
        */

        /*
        ListNode* mergeKLists(vector<ListNode*>& lists) {
            if(lists.size() == 0){
                return NULL;
            }
            int len = lists.size();
            for(int distance = len / 2; distance > 0; distance /= 2){
                int i;
                for(i = 0; i < distance; i++){
                    lists[i] = mergeTwo(lists[i], lists[i+distance]);
                }
                if(i+distance < len){
                   lists[0] = mergeTwo(lists[0], lists[i+distance]);
                }
                len /= 2;
            }

            return lists[0];
        }
        */


        ListNode* mergeKLists(vector<ListNode*>& lists) {
            if(lists.size() == 0){
                return NULL;
            }
            queue<ListNode*> con;
            for(int i = 0; i < lists.size(); i++){
                con.push(lists[i]);
            }

            while(con.size() > 1){
                ListNode *p = con.front();
                con.pop();
                ListNode *q = con.front();
                con.pop();
                con.push(mergeTwo(p, q));
            }

            return con.front();
        }

    };
