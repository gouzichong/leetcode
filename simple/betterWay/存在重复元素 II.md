# Leetcode 219
    class Solution {
    public:
        /*
        bool containsNearbyDuplicate(vector<int>& nums, int k) {
            unordered_map<int, int> con;
            int i;
            for(i = 0; i < nums.size(); i++){
                if(con[nums[i]]){
                    if(i + 1 - con[nums[i]] <= k){
                        return true;
                    }
                }
                con[nums[i]] = i + 1;
            }

            return false;
        }
        */
        bool containsNearbyDuplicate(vector<int>& nums, int k) {
            unordered_set<int> con;
            int i;
            for(i = 0; i < nums.size(); i++){
                if(con.count(nums[i])){
                    return true;
                }
                con.insert(nums[i]);
                if(con.size() > k){
                    con.erase(nums[i-k]);
                }
            }

            return false;
        }
    };
