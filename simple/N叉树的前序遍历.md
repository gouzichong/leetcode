# Leetcode 589
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

            /* 递归
            void preOrderOneNode(Node* root, vector<int>& ret){
                int size = 0, i;
                if(root == NULL)
                    return;

                ret.push_back(root->val);
                for(i = 0; i < root->children.size(); i++){
                    preOrderOneNode(root->children[i], ret);
                }
            }



            vector<int> preorder(Node* root) {
                vector<int> ret;

                preOrderOneNode(root, ret);

                return ret;
            }
            */

            //迭代
            vector<int> preorder(Node* root) {
                int i;
                vector<int> ret;
                stack<Node*> tmp;

                if(root == NULL)
                    return ret;
                tmp.push(root);

                while(!tmp.empty()){
                    Node *front = tmp.top();
                    tmp.pop();
                    ret.push_back(front->val);

                    for(i = front->children.size() - 1; i >= 0; i--){
                        tmp.push(front->children[i]);
                    }
                }

                return ret;
            }
        };
