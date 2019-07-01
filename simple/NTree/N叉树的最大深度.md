# Leetcode 559
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
        void findCurNodeDepth(Node* root, int& depth){
            if(root == NULL)
                return;

            int i, childDepth, tmp;

            depth++;
            childDepth = tmp = depth;
            for(i = 0; i < root->children.size(); i++){
                findCurNodeDepth(root->children[i], childDepth);
                if(childDepth > depth)
                    depth = childDepth;
                childDepth = tmp;
            }
        }

        int maxDepth(Node* root) {
            int ret = 0;

            findCurNodeDepth(root, ret);

            return  ret;
        }
    };
