# Leetcode 961
    class Solution {
    public:
        int repeatedNTimes(vector<int>& A) {
            //int repeatTime = A.size() / 2;
            int i;
            //set<int> tmp;

            /*
            for(i = 0; i < repeatTime + 2; i++){
                if(tmp.find(A[i]) == tmp.end())
                    tmp.insert(A[i]);
                else{
                    break;
                }
            }
            */

            for(i = 0; i < A.size()-1; i++){
                if(A[i] == A[i+1])
                    return A[i];
            }

            if(A[1] == A[3])
                return A[1];

            return A[0];

        }
    };
