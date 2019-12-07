# Leetcode 69
    class Solution {
    public:
        /*
        int mySqrt(int x) {
            long int i;
            int ret = 0;
            long int value = 0;
            for(i = 1; i <= x; i++){
                value = i * i;
                if(value >= x){
                    if(i * i == x){
                        ret = i;
                    }else{
                        ret = i - 1;
                    }
                    break;
                }
            }

            return ret;
        }
        */
        int mySqrt(int x) {
            long int begin = 0, end = x;
            long int mid;
            while(begin <= end){
                mid = begin + (end - begin) / 2;
                if(mid * mid > x){
                    end = mid - 1;
                }else{
                    begin = mid + 1;
                }
            }

            return begin - 1;
        }
    };
