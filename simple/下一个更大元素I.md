# Leetcode 496
    class Solution {
    public:
        vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
    /*
            vector<int> ret;
            vector<int>::iterator iter;
            int i, j;

            for(i = 0; i < nums1.size(); i++){
                iter = find(nums2.begin(), nums2.end(), nums1[i]);
                for(j = iter-nums2.begin(); j < nums2.size(); j++){
                    if(nums2[j] > nums1[i]){
                        ret.push_back(nums2[j]);
                        break;
                    }
                    if(j == nums2.size() - 1)
                        ret.push_back(-1);
                }
            }

            return ret;
    */

            vector<int> ret;
            unordered_map<int, int> table;
            int i, j;

            if(nums1.size() == 0)
                return ret;
            for(i = 0; i < nums2.size(); i++){
                for(j = i + 1; j < nums2.size(); j++){
                    if(nums2[j] > nums2[i]){
                        table[nums2[i]] = nums2[j];
                        break;
                    }
                    if(j == nums2.size() - 1)
                        table[nums2[i]] = -1;
                }
            }

            table[nums2[nums2.size()-1]] = -1;
            for(i = 0; i < nums1.size(); i++){
                ret.push_back(table[nums1[i]]);
            }

            return ret;
        }
    };
