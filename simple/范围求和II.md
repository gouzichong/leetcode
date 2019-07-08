# Leetcode 598
    class Solution {
    public:
        int maxCount(int m, int n, vector<vector<int>>& ops) {
            int minI, minJ, i;
            if(ops.size() < 1)
                return m * n;

            minI = ops[0][0];
            minJ = ops[0][1];

            for(i = 1; i < ops.size(); i++){
                if(ops[i][0] < minI)
                    minI = ops[i][0];
                if(ops[i][1] < minJ)
                    minJ = ops[i][1];
            }


            return minI * minJ;
        }
    };
