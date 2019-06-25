# Leetcode 122
    class Solution {
    public:
        int maxProfit(vector<int>& prices) {
    /*
            if(prices.size() == 0)
                return 0;

            int i, j, begin = -1, end = -1, ret = 0;

            for(i = 0; i < prices.size() - 1; i++){
                if(begin == -1 && prices[i] < prices[i+1]){
                    begin = prices[i];
                    continue;
                }

                if(prices[i] > prices[i+1] && begin != -1){
                    end = prices[i];
                }

                if(end != -1){
                    ret += end - begin;
                    begin = -1;
                    end = -1;
                }


            }

            if(begin != -1 && end == -1){
                ret += prices[i] - begin;
            }

            return ret;
    */

            if(prices.size() == 0)
                return 0;

            int i, ret = 0;

            for(i = 0; i < prices.size() - 1; i++){
                if(prices[i] < prices[i+1])
                    ret += prices[i+1] - prices[i];
            }



            return ret;
        }
    };
