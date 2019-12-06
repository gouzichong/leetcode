# Leetcode 111
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
        int preOrder(TreeNode *root, int cur){
            cur++;
            if(root->left == NULL && root->right == NULL){
                return cur;
            }

            int leftdepth = 0;
            int rightdepth = 0;
            if(root->left){
                leftdepth = preOrder(root->left, cur);
            }
            if(root->right){
                rightdepth = preOrder(root->right, cur);
            }

            if(!rightdepth){
                return leftdepth;
            }

            if(!leftdepth){
                return rightdepth;
            }

            return min(leftdepth, rightdepth);
        }

        int minDepth(TreeNode* root) {
            if(root == NULL){
                return 0;
            }

            return preOrder(root, 0);
        }
        */


        int minDepth(TreeNode* root) {
            if(root == NULL){
                return 0;
            }
            int leftDepth = minDepth(root->left);
            int rightdepth = minDepth(root->right);

            if(leftDepth == rightdepth && leftDepth == 0){
                return 1;
            }
            if(!leftDepth){
                return rightdepth + 1;
            }
            if(!rightdepth){
                return leftDepth + 1;
            }

            return min(leftDepth, rightdepth) + 1;
        }

    };
