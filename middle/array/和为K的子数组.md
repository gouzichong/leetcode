# Leetcode 560
    class Solution {
    public:
        /*
        int subarraySum(vector<int>& nums, int k) {
            int ret = 0;

            int preSum[nums.size()+1] = {0};
            for(int i = 1; i <= nums.size(); i++){
                preSum[i] = preSum[i-1] + nums[i-1];
            }

            for(int i = 0; i < nums.size(); i++){
                for(int j = i + 1; j <= nums.size(); j++){
                    if(preSum[j] - preSum[i] == k){
                        ret++;
                    }
                }
            }

            return ret;
        }
        */

        /*//暴力
        int subarraySum(vector<int>& nums, int k) {
            int ret = 0;

            for(int i = 0; i < nums.size(); i++){
                int sum = 0;
                for(int j = i; j < nums.size(); j++){
                    sum += nums[j];
                    if(sum == k){
                        ret++;
                    }
                }
            }

            return ret;
        }
        */


        int subarraySum(vector<int>& nums, int k) {
            int ret = 0;

            int sum = 0;
            for(int i = 0; i < nums.size(); i++){
                sum += nums[i];
                int j = 0;
                int tmp = sum;
                while(j <= i){
                    if(tmp == k){
                        ret++;
                    }
                    tmp -= nums[j];
                    j++;
                }
            }

            return ret;
        }

        /*//哈希
        int subarraySum(vector<int>& nums, int k) {
            int ret = 0;

            unordered_map<int, int> sumToTime;
            sumToTime[0] = 1;

            int sum = 0;
            for(int i = 0; i < nums.size(); i++){
                sum += nums[i];
                if(sumToTime.count(sum - k)){
                    ret += sumToTime[sum-k];
                }
                sumToTime[sum]++; 
            }

            return ret;
        }
        */

    };
