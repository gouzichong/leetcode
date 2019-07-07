# Leetcode 541
    class Solution {
    public:
        string reverseStr(string s, int k) {
            int begin, end, time = 0;
            char tmp;

            begin = 0;
            end = k < s.size() ? k - 1 : s.size() - 1;

            while(begin < end){
                tmp = s[end];
                s[end] = s[begin];
                s[begin] = tmp;
                begin++;
                end--;

                if(begin >= end){
                    time += 2;
                    begin = time * k;
                    if(begin > s.size() - 1)
                        break;
                    end = time * k + k < s.size() ? time * k + k - 1 : s.size() - 1;
                }
            }

            return s;
        }
    };
