# Leetcode 429
    /*
    // Definition for a Node.
    class Node {
    public:
        int val;
        vector<Node*> children;

        Node() {}

        Node(int _val, vector<Node*> _children) {
            val = _val;
            children = _children;
        }
    };
    */
    class Solution {
    public:
        vector<vector<int>> levelOrder(Node* root) {  
            vector<vector<int>> ret;
            vector<int> tmp;
            queue<Node*> parent, child;
            int i;

            if(root == NULL)
                return ret;

            parent.push(root);

            while(!parent.empty()){
                tmp.clear();
                while(!child.empty()){
                    child.pop();
                } 
                while(!parent.empty()){
                    root = parent.front();
                    tmp.push_back(root->val);
                    parent.pop();
                    for(i = 0; i < root->children.size(); i++){
                        child.push(root->children[i]);
                    }
                }

                ret.push_back(tmp);
                parent = child;
            }

            return ret;
        }
    };
