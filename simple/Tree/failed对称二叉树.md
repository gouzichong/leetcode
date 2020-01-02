# Leetcode 101
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
        bool recurFun(TreeNode* left, TreeNode* right){
            if(left == NULL && right == NULL){
                return true;
            }

            if((left == NULL && right != NULL) || (left != NULL && right == NULL) || (left->val != right->val)){
                return false;
            }

            return recurFun(left->left, right->right) && recurFun(left->right, right->left);
        }

        bool isSymmetric(TreeNode* root) {
            if(root == NULL){ 
                return true;
            }
            //递归
            //return recurFun(root->left, root->right);


            //迭代
            queue<TreeNode*> left, right;
            TreeNode *leftNode, *rightNode;

            left.push(root->left);
            right.push(root->right);

            while(!left.empty() && !right.empty()){
                leftNode = left.front();
                rightNode = right.front();
                left.pop();
                right.pop();

                if((!leftNode && rightNode) || (leftNode && !rightNode)){
                    return false;
                }

                if(leftNode){
                    if(leftNode->val != rightNode->val){
                        return false;
                    }
                    left.push(leftNode->left);
                    left.push(leftNode->right);
                    right.push(rightNode->right);
                    right.push(rightNode->left);
                }
            }

            return true;
        }
    };
