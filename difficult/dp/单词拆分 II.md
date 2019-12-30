# Leetcode 140
    class Solution {
    public:
        /* 
        //递归超时
        vector<string> helper(string& s, unordered_set<string>& con, int start){
            vector<string> ret;
            if(start == s.size()){
                ret.push_back("");
            }
            for(int end = start + 1; end <= s.size(); end++){
                string cur = s.substr(start, end-start);
                if(con.count(cur)){
                    vector<string> tmp = helper(s, con, end);
                    for(auto v : tmp){
                        ret.push_back(cur + (v == "" ? "" : " ") + v);
                    }
                }
            }
            return ret;
        }

        vector<string> wordBreak(string s, vector<string>& wordDict) {
            unordered_set<string> con(wordDict.begin(), wordDict.end());
            return helper(s, con, 0);
        }
        */

        /*
        //记忆法递归
        vector<string> helper(string& s, unordered_set<string>& con, int start, unordered_map<int, vector<string>>& dp){
            if(dp.count(start)){
                return dp[start];
            }
            vector<string> ret;
            if(start == s.size()){//到了最后，说明一定可以拆分
                ret.push_back("");
            }
            for(int end = start + 1; end <= s.size(); end++){
                string cur = s.substr(start, end-start);
                if(con.count(cur)){
                    cout << cur << endl;
                    vector<string> tmp = helper(s, con, end, dp);
                    for(auto v : tmp){
                        ret.push_back(cur + (v == "" ? "" : " ") + v);
                    }
                }
            }
            dp[start] = ret;
            return ret;
        }

        vector<string> wordBreak(string s, vector<string>& wordDict) {
            unordered_set<string> con(wordDict.begin(), wordDict.end());
            unordered_map<int, vector<string>> dp;
            return helper(s, con, 0, dp);
        }
        */

        /*
        //dp超时
        vector<string> wordBreak(string s, vector<string>& wordDict) {
            unordered_set<string> con(wordDict.begin(), wordDict.end());
            vector<vector<string>> dp(s.size()+1);
            dp[0].push_back("");

            for(int i = 1; i <= s.size(); i++){
                vector<string> tmp;
                for(int j = 0; j < i; j++){
                    string cur = s.substr(j, i-j);
                    if( dp[j].size() > 0 && con.count(cur) ){
                        for(auto v : dp[j]){
                            tmp.push_back(v + (v == "" ? "" : " ") + cur);
                        }
                    }
                }
                dp[i] = tmp;
            }
            return dp[s.size()];
        }
        */

         /*//dp2超时
        vector<string> wordBreak(string s, vector<string>& wordDict) {
            int size = s.size();
            vector<vector<string>> dp(size+1);
            dp[size].push_back("");


            for(int i = size - 1; i >= 0; i--){
                for(int j = 0; j < wordDict.size(); j++){
                    int end = i + wordDict[j].size();
                    if(end <= size && dp[end].size() > 0 && s.substr(i, end-i) == wordDict[j]){
                        for(auto v : dp[end]){
                            dp[i].push_back(s.substr(i, end-i) + (v == "" ? "" : (" " + v)));
                        }
                    }
                }
            }

            return dp[0];
        }
        */   

        /*
        //记忆法递归二
        vector<string> helper(string remain, vector<string>& wordDict, unordered_map<string, vector<string>> &dp){
            if(dp.count(remain)){
                return dp[remain];
            }

            if(remain.empty()){//到了最后，说明一定可以拆分
                return {""};
            }

            vector<string> ret;
            for(int i = 0; i < wordDict.size(); i++){
                if(remain.substr(0, wordDict[i].size()) == wordDict[i]){
                    vector<string> tmp = helper(remain.substr(wordDict[i].size()), wordDict, dp);
                    for(auto v : tmp){
                        ret.push_back(wordDict[i] + (v == "" ? "" : " ") + v);
                    }
                }
            }
            dp[remain] = ret;
            return ret;
        }

        vector<string> wordBreak(string s, vector<string>& wordDict) {
            unordered_map<string, vector<string>> dp;
            return helper(s, wordDict, dp);
        }
        */


        //前缀树+dfs+动态规划
        struct treeNode{
            int flag;//a word end flag
            map<char, treeNode*> next;
            treeNode() : 
                flag(false)
            {}
        };

        treeNode* buildPreTree(vector<string> &wordDict){
            treeNode *root = new treeNode();
            treeNode *cur;
            for(auto &w : wordDict){
                cur = root;
                for(auto c : w){
                    if(!cur->next.count(c)){
                        cur->next[c] = new treeNode();
                    }
                    cur = cur->next[c];
                }
                cur->flag = true;
            }
            return root;
        }

        void dfs(string &s, vector<vector<int>> &dp, int i, vector<string> &v, vector<string> &res){
            if(i == 0){
                string t;
                for(auto iter = v.rbegin(); iter != v.rend(); ++iter){
                    t += *iter + " ";
                }
                t.pop_back();
                res.push_back(t);
                return;
            }

            for(auto j : dp[i]){
                v.push_back(s.substr(j, i-j));
                dfs(s, dp, j, v, res);
                v.pop_back();
            }
        }

        vector<string> wordBreak(string s, vector<string>& wordDict) {
            treeNode *root = buildPreTree(wordDict);

            int size = s.size();
            vector<vector<int>> dp(size+1);
            dp[0].push_back(-1);
            for(int i =  0; i < size; i++){
                if(!dp[i].empty()){
                    int j = i;
                    treeNode *node = root;
                    while(j < size && node->next.count(s[j])){
                        node = node->next[s[j++]];
                        if(node->flag){
                            dp[j].push_back(i); //以i开始，以j结尾的字符串
                        }
                    }       
                }
            }

            vector<string> cur;
            vector<string> ret;
            dfs(s, dp, size, cur, ret);
            return ret;
        }
    };
