# Leetcode 350
    class Solution {
    public:
        vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {

            vector<int> ret;
            int i, j;

            sort(nums1.begin(), nums1.end());
            sort(nums2.begin(), nums2.end());

            i = 0;
            j = 0;
            while(i < nums1.size() && j < nums2.size()){
                if(nums1[i] < nums2[j]){
                    i++;
                }else if(nums1[i] > nums2[j]){
                    j++;
                }else{
                    ret.push_back(nums1[i]);
                    i++;
                    j++;
                }
            }

            return ret;

    /*
            unordered_map<int, int> container;
            vector<int> ret;
            int i;

            for(i = 0; i < nums1.size(); i++){
                container[nums1[i]]++;
            }

            for(i = 0; i < nums2.size(); i++){
                if(container[nums2[i]]){
                    ret.push_back(nums2[i]);
                    container[nums2[i]]--;
                }
            }

            return ret;
    */
        }
    };
