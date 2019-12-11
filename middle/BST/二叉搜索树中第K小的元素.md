# Leetcode 230
    /**
     * Definition for a binary tree node.
     * struct TreeNode {
     *     int val;
     *     TreeNode *left;
     *     TreeNode *right;
     *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
     * };
     */
    class Solution {
    public:
        /*
        void inOrder(TreeNode *root, vector<int> &con){
            if(root == NULL){
                return;
            }

            inOrder(root->left, con);
            con.push_back(root->val);
            inOrder(root->right, con);
        }

        int kthSmallest(TreeNode* root, int k) {
            vector<int> con;
            inOrder(root, con);
            return con[k-1];
        }
        */
        /*
        void inOrder(TreeNode *root, int& count, int& ret){
            if(root == NULL){
                return;
            }

            inOrder(root->left, count, ret);
            count--;
            if(count  == 0){
                ret = root->val;
                return;
            }
            inOrder(root->right, count, ret);
        }

        int kthSmallest(TreeNode* root, int k) {
            int ret;
            inOrder(root, k, ret);
            return ret;
        }
        */

        int kthSmallest(TreeNode* root, int k) {
            stack<TreeNode*> con;
            int num = 0;
            TreeNode *cur = root;
            while(!con.empty() || cur){
                if(cur){
                    con.push(cur);
                    cur = cur->left;
                }else{
                    cur = con.top();
                    con.pop();
                    num++;
                    if(num == k){
                        return cur->val;
                    }
                    cur = cur->right;
                }
            }

            return 0;
        }

    };
