# Leetcode 532
    class Solution {
    public:
        int findPairs(vector<int>& nums, int k) {
            if(k < 0){
                return 0;
            }
            unordered_map<int, int> con;

            for(int i = 0; i < nums.size(); i++){
                con[nums[i]] = i;
            }

            int ret = 0;
            for(int i = 0; i < nums.size(); i++){
                if(con.count(nums[i]+k) && con[nums[i]+k] != i){
                    ret++;
                    con.erase(nums[i]+k);
                }
            }


            return ret;
        }
    };
