# Leetcode 590
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
        void postOrderOneNode(Node* root, vector<int>& ret){

            int i = 0;
            if(root == NULL)
                return;

            if(root->children.empty()){
                ret.push_back(root->val);
                return;
            }

            for(i = 0; i < root->children.size(); i++){
                postOrderOneNode(root->children[i], ret);
            }


            ret.push_back(root->val);
        }
        vector<int> postorder(Node* root) {
            vector<int> ret;

            postOrderOneNode(root, ret);

            return ret;
        }

        */


        vector<int> postorder(Node* root) {
            int i;
            vector<int> ret;
            stack<Node*> tmp;
            set<Node*> tmp1;
            Node* temp;
            if(root == NULL)
                return ret;

            tmp.push(root);  

            while(!tmp.empty()){
                temp = tmp.top();
                if(tmp1.find(temp) == tmp1.end()){
                    tmp1.insert(temp);
                    for(i = temp->children.size()-1; i >= 0; i--)
                        tmp.push(temp->children[i]);
                    continue;
                }

                ret.push_back(temp->val);
                tmp.pop();

            }

            return ret;
        }
    };
