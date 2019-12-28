# Leetcode 227
    class Solution {
    public:
        int calculate(string s) {
            int md = -1; //0代表乘，1是除
            int sign = 1;//默认是加
            int prev = 0;
            int ret = 0;

            for(int i = 0; i < s.size(); i++){
                if(isdigit(s[i])){
                    int num = s[i] - '0';
                    while(++i < s.size() && isdigit(s[i])){
                        num = num*10 + (s[i] - '0');
                    }
                    i--;
                    if(md == 0){
                        prev *= num;
                        md = -1;
                    }else if(md == 1){
                        prev /= num;
                        md = -1;
                    }else{
                        prev = num;
                    }
                }else if(s[i] == '/'){
                    md = 1;
                }else if(s[i] == '*'){
                    md = 0;
                }else if(s[i] == '+'){
                    ret = ret + sign * prev;
                    sign = 1;
                }else if(s[i] == '-'){
                    ret = ret + sign * prev;
                    sign = -1;
                }
            }

            return ret + sign * prev;
        }
    };
