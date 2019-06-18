# Leetcode 171
    class Solution {
    public:
        int titleToNumber(string s) {
            int i, ret = 0;
            int len;

            for(i = s.length()-1; i >= 0; i--){
                len = s[i] - 'A' + 1;
                ret += len * pow(26, (s.length()-i-1));
            }

            return ret;
        }
    };
