# Leetcode 1005
    class Solution {
    public:
        int largestSumAfterKNegations(vector<int>& A, int K) {
            int i, sum;


            sort(A.begin(), A.end());

            i = 0;
            while(i < K){
                if(A[i] < 0){
                    A[i] = -A[i];
                    i++;
                    continue;
                }
                break;
            }

            if((K - i) % 2 != 0){
                if(i > 0 && A[i] > A[i-1]){
                    A[i-1] = -A[i-1];
                }else{
                    A[i] = -A[i];
                }
            }

            sum = 0;
            for(i = 0; i < A.size(); i++){
                sum += A[i];
            }


            return sum;
        }
    };
