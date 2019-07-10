# Leetcode 551
    class Solution {
    public:
        bool checkRecord(string s) {
    /*
            int i;
            int A = 0, L = 0;

            i = 0;
            while(i < s.size()){
                if(s[i] == 'A'){
                    A++;
                }else if(s[i] == 'L'){
                    while(i < s.size() && s[i] == 'L'){
                        L++;
                        i++;
                    }

                    if(L > 2)
                        return false;
                    L = 0;
                    continue;
                }

                i++;
                if(A > 1)
                    return false;
            }

            return true;
    */
            int i = 0;
            int A = 0, L = 0;

            for(i = 0; i < s.size(); i++){
                if(s[i] == 'L'){
                    L++;
                    if(L == 3)
                        return false;
                }else{            
                    if(s[i] == 'A')
                        A++;
                    if(A > 1)
                        return false;
                    L = 0;                
                }
            }

            return true;
        }
    };
