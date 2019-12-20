# Leetcode 454
    class Solution {
    public:
        int fourSumCount(vector<int>& A, vector<int>& B, vector<int>& C, vector<int>& D) {
            unordered_map<int, int> ABSum;
            for(int i = 0; i < A.size(); i++){
                for(int j = 0; j < B.size(); j++){
                    ABSum[A[i]+B[j]]++;
                }
            }

            int ret = 0;
            for(int i = 0; i < C.size(); i++){
                for(int j = 0; j < D.size(); j++){
                    if(ABSum[-C[i]-D[j]]){
                        ret += ABSum[-C[i]-D[j]];
                    }
                }
            }

            return ret;
        }
    };
