# Leetcode 643
    class Solution {
    public:
        double findMaxAverage(vector<int>& nums, int k) {
            int begin;
            double sum = 0;
            for(begin = 0; begin < k; begin++){
                sum += nums[begin];
            }

            begin = 0;
            int end = k;
            int curSum = sum;
            while(end < nums.size()){
                curSum = curSum- nums[begin] + nums[end];
                if(curSum > sum){
                    sum = curSum;
                }
                begin++;
                end++;
            }

            return sum / k;
        }
    };
