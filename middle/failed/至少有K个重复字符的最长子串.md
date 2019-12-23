# Leetcode 395
    class Solution {
    public:
        int helper(string &s, int k, int left, int right){
            if(right - left + 1 < k){
                return 0;
            }

            int con[26] = {0};
            for(int i = left; i <= right; i++){
                con[s[i]-'a']++;
            }

            while(right - left + 1 >= k && con[s[left]-'a'] < k){
                left++;
            }

            while(right - left + 1 >= k && con[s[right]-'a'] < k){
                right--;
            }

            if(right - left + 1  < k){
                return 0;
            }

            for(int i = left; i <= right; i++){
                if(con[s[i]-'a'] < k){
                    return max(helper(s, k, left, i-1), helper(s, k, i+1, right));//直接返回因为此时包含s[i]的一定不符合
                }
            }

            return right - left + 1;
        }

        int longestSubstring(string s, int k) {
            return helper(s, k, 0, s.size() - 1);
        }
    };
