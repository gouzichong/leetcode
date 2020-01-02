# Leetcode 107
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
        vector<vector<int>> levelOrderBottom(TreeNode* root) {
            queue<TreeNode*> parent, child;
            vector<vector<int>> ret;
            vector<int> element;
            vector<vector<int>>::iterator begin;

            if(root == NULL)
                return ret;

            parent.push(root);


            while(!parent.empty()){
                begin = ret.begin();
                element.clear();
                while(!child.empty()){
                    child.pop();
                }

                while(!parent.empty()){
                    if(parent.front()->left != NULL)
                        child.push(parent.front()->left);
                    if(parent.front()->right != NULL)
                        child.push(parent.front()->right);
                    element.push_back(parent.front()->val);
                    parent.pop();
                }
                parent = child;
                ret.insert(begin, element);
            }

            return ret;
        }
    };
