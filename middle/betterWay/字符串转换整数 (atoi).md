# Leetcode 8
    class Solution {
    public:
        /*
        int stringToInt(string num, bool negative){
            long ret = 0;
            for(int i = 0; i < num.size(); i++){
                ret *= 10;
                ret += num[i] - '0';
            }

            if(negative && ret > 2147483648){
                return INT_MIN;
            }

            if(!negative && ret > INT_MAX){
                return INT_MAX;
            }

            return negative ? -ret : ret;
        }
        */

        int stringToInt(string num, bool negative){
            int ret = 0;
            for(int i = 0; i < num.size(); i++){
                int cur = num[i] - '0';
                if(ret > INT_MAX / 10 || (ret == INT_MAX / 10 && cur > 7)){
                    return negative ? INT_MIN : INT_MAX;
                }
                ret *= 10;
                ret += cur;
            }

            return negative ? -ret : ret;
        }


        int myAtoi(string str) {
            bool negative = false;
            int i = 0;

            while(str[i] == ' '){
                i++;
            }

            if(str[i] == '+' || str[i] == '-'){
                if(str[i] == '-'){
                    negative = true;
                }
                i++;
            }


            if(isdigit(str[i]) == 0){
                return 0;
            }

            while(str[i] == '0'){
                i++;
            }

            int len = 0;
            int begin = i;
            while(isdigit(str[i])){
                i++;
                len++;
            }

            if(len > 10){
                return negative ? INT_MIN : INT_MAX;
            }

            return stringToInt(str.substr(begin, len), negative);
        }
    };
