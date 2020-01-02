# Leetcode 671
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
        int findSecondMin(TreeNode* root, int rootVal){
            if(root == NULL)
                return -1;

            if(root->val != rootVal){
                return root->val;
            }else{
                int minLeft = findSecondMin(root->left, rootVal);
                int minRight = findSecondMin(root->right, rootVal);    

                if(minLeft != -1 && minRight != -1){
                    return min( minLeft, minRight);
                }else if(minLeft != -1){
                    return minLeft;
                }else{
                    return minRight;
                }
            }
        }
        */
        int findSecondMinimumValue(TreeNode* root) {
            //better 递归
            if(root == NULL || root->left == NULL)
                return -1;

            int leftMin = root->left->val;
            int rightMin = root->right->val;

            if(leftMin == root->val){
                leftMin = findSecondMinimumValue(root->left);
            }

            if(rightMin == root->val){
                rightMin = findSecondMinimumValue(root->right);
            }

            if(leftMin != -1 && rightMin != -1){
                return min(leftMin, rightMin);
            }

            if(leftMin != -1){
                return leftMin;
            }

            return rightMin;


            /* //递归2
            if(root == NULL)
                return -1;

            if(root->left){
                if(root->left->val != root->val && root->right->val != root->val){
                    return min(root->left->val, root->right->val);
                }else if(root->left->val != root->val){
                    int rightMin = findSecondMinimumValue(root->right);
                    return rightMin != -1 && rightMin < root->left->val ? rightMin : root->left->val;
                }else if(root->right->val != root->val){
                    int leftMin = findSecondMinimumValue(root->left);
                    return leftMin != -1 && leftMin < root->right->val ? leftMin : root->right->val;               
                }else{
                    int leftMin = findSecondMinimumValue(root->left);
                    int rightMin = findSecondMinimumValue(root->right);
                    if(leftMin != -1 && rightMin != -1){
                        return min(leftMin, rightMin);
                    }else if(leftMin != -1){
                        return leftMin;
                    }else{
                        return rightMin;
                    }

                }
            }else{
                return -1;
            }
            */
            // 递归1
            //return findSecondMin(root, root->val);


    /*      //迭代
            stack<TreeNode*> container;
            TreeNode* tmp;
            int curMax, rootVal;

            if(root == NULL){
                return -1;
            }

            container.push(root);        
            rootVal = root->val;
            curMax = -1;

            while(!container.empty()){
                tmp = container.top();
                container.pop();

                if(tmp->val != rootVal && (tmp->val < curMax || curMax == -1)){
                    curMax = tmp->val;
                }

                if(tmp->val == rootVal && tmp->left){
                    container.push(tmp->right);
                    container.push(tmp->left);
                }

            }

            return curMax;
    */
        }
    };
