# Leetcode 337
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
        /*//暴力递归
        int rob(TreeNode* root) {
            if(root == NULL){
                return 0;
            }

            int leftChild = rob(root->left);
            int rightChild = rob(root->right);

            int grandChildSum = 0;
            if(root->left && root->right){
                grandChildSum = rob(root->left->left) + rob(root->left->right) + rob(root->right->left) + rob(root->right->right);
            }else if(root->left){
                grandChildSum = rob(root->left->left) + rob(root->left->right);
            }else if(root->right){
                grandChildSum = rob(root->right->left) + rob(root->right->right);
            }


            return max(leftChild + rightChild, root->val + grandChildSum);
        }
        */
        /*//记忆法+递归
        int dfs(TreeNode *root, unordered_map<TreeNode*, int> &con)
        {
            if(root == NULL){
                return 0;
            }
            if(con.count(root)){
                return con[root];
            }

            int leftChild = dfs(root->left, con);
            int rightChild = dfs(root->right, con);

            int grandChildSum = 0;
            if(root->left){
                grandChildSum += dfs(root->left->left, con) + dfs(root->left->right, con);
            }

            if(root->right){
                grandChildSum += dfs(root->right->left, con) + dfs(root->right->right, con);
            }
            con[root] = max(leftChild + rightChild, root->val + grandChildSum);

            return con[root];        
        }

        int rob(TreeNode* root) {
            if(root == NULL){
                return 0;
            }
            unordered_map<TreeNode*, int> con;

            return dfs(root, con);
        }
        */

        //递归+dp
        pair<int, int> dfs(TreeNode *root)
        {
            if(root == NULL){
                return {0, 0};
            }

            pair<int, int> leftChild = dfs(root->left);
            pair<int, int> rightChild = dfs(root->right);


            return {root->val + leftChild.second + rightChild.second, max(leftChild.first, leftChild.second) + max(rightChild.first, rightChild.second)};        
        }

        int rob(TreeNode* root) {
            if(root == NULL){
                return 0;
            }
            pair<int, int> ret = dfs(root);//first表示选了当前节点，second表示不选当前节点

            return max(ret.first, ret.second);
        }
    };
