# Leetcode 922
    class Solution {
    public:
        vector<int> sortArrayByParityII(vector<int>& A) {
            int i, jE = 0, jO = 1;
            vector<int> ret(A.size());

            for(i = 0; i < A.size(); i++){
                if(A[i] % 2 == 0){
                    ret[jE] = A[i];
                    jE += 2;
                }else{
                    ret[jO] = A[i];
                    jO += 2;
                }
            }

            return ret;
        }
    };
