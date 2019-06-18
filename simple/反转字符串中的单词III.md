# Leetcode 557
    class Solution {
    public:
        string reverseWords(string s) {
            int i, j, lastEnd = -1;
            string ret;


            for(i = 0; i < s.length(); i++){
                if(s[i] == ' '){
                    for(j = i-1; j > lastEnd; j--){
                        ret.append(1, s[j]);
                    }
                    ret.append(1, s[i]);
                    lastEnd = i;
                }
            }

            for(j = i-1; j > lastEnd; j--){
                    ret.append(1, s[j]);
            }
            return ret;
        }
    };
