# Leetcode 212
    class Solution {
    public:
        struct trieNode{
            bool isWord;
            string word;
            map<char, trieNode*> next;
            trieNode() :
                isWord(false)
            {}
        };

        trieNode* buildTree(vector<string> &words){
            trieNode *root = new trieNode();
            trieNode *cur;
            for(string &w : words){
                cur = root;
                for(char c : w){
                    if(!cur->next.count(c)){
                        cur->next[c] = new trieNode();
                    }
                    cur = cur->next[c];
                }
                cur->isWord = true;
                cur->word = w;
            }
            return root;
        }

        void dfs(vector<string> &ret, vector<vector<char>>& board, trieNode* root, int x, int y){
            if(root->isWord){
                ret.push_back(root->word);
                root->isWord = false;
            }

            if(x < 0 || x >= board.size() || y < 0 || y >= board[0].size()){
                return;
            }

            if(!root->next.count(board[x][y])){
                return;
            }

            char cur = board[x][y];
            board[x][y] = '#';
            dfs(ret, board, root->next[cur], x, y-1);
            dfs(ret, board, root->next[cur], x, y+1);
            dfs(ret, board, root->next[cur], x-1, y);
            dfs(ret, board, root->next[cur], x+1, y);
            board[x][y] = cur;
        }

        vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
            trieNode *root = buildTree(words);
            vector<string> ret;

            for(int i = 0; i < board.size(); i++){
                for(int j = 0; j < board[0].size(); j++){
                    dfs(ret, board, root, i, j);
                }
            }

            return ret;
        }
    };
