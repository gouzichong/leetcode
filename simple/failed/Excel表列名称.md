# Leetcode 168
    class Solution {
    public:
        string convertToTitle(int n) {
            string ret;

            while(n > 0){
                n--;
                ret.push_back('A'+n % 26);
                n /= 26;
            }

            reverse(ret.begin(), ret.end());
            return ret;
        }
    };
