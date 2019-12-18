# Leetcode 208
    class Trie {
    public:
        /** Initialize your data structure here. */
        Trie() {
            preTree = new Node();
        }

        /** Inserts a word into the trie. */
        void insert(string word) {
            int i;
            Node *cur = preTree;
            for(i = 0; i < word.size(); i++){
                if(cur->child[word[i]-'a'] == NULL){
                    break;
                }
                cur = cur->child[word[i]-'a'];
            }

            while(i < word.size()){
                cur->child[word[i]-'a'] = new Node();
                cur = cur->child[word[i]-'a'];
                i++;
            }
            cur->isString = true;
        }

        /** Returns if the word is in the trie. */
        bool search(string word) {
            Node *cur = preTree;
            int i;
            for(i = 0; i < word.size(); i++){
                if(cur->child[word[i]-'a'] == NULL){
                    return false;
                }
                cur = cur->child[word[i]-'a'];
            }

            return cur->isString;
        }

        /** Returns if there is any word in the trie that starts with the given prefix. */
        bool startsWith(string prefix) {
            Node *cur = preTree;
             for(int i = 0; i < prefix.size(); i++){
                if(cur->child[prefix[i]-'a'] == NULL){
                    return false;
                }
                cur = cur->child[prefix[i]-'a'];
            }

            return true;       
        }


        struct Node{
            bool isString;
            //vector<Node*> child;    
            //Node* child[26] = {NULL};
            Node* child[26];
            Node(){
                isString = false;
                memset(child, 0, sizeof(child));
                //child.resize(26);
                //child = new Node *[26];
            }
        };

        Node *preTree;
    };

    /**
     * Your Trie object will be instantiated and called as such:
     * Trie* obj = new Trie();
     * obj->insert(word);
     * bool param_2 = obj->search(word);
     * bool param_3 = obj->startsWith(prefix);
     */
