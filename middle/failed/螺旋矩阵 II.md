# Leetcode 59
    class Solution {
    public:
        vector<vector<int>> generateMatrix(int n) {
            int size = n * n;
            int rowBegin = 0;
            int rowEnd = n - 1;
            int colomnBegin = 0;
            int colomnEnd = n - 1;

            vector<vector<int>> ret(n, vector<int>(n));
            int i = 1;
            while(i <= size){
                for(int y = colomnBegin; y <= colomnEnd; y++){
                    ret[rowBegin][y] = i++;
                }

                for(int x = rowBegin + 1; x <= rowEnd; x++){
                    ret[x][colomnEnd] = i++;
                }

                for(int y = colomnEnd - 1; y >= colomnBegin; y--){
                    ret[rowEnd][y] = i++;
                }

                for(int x = rowEnd - 1; x > colomnBegin; x--){
                    ret[x][rowBegin] = i++;
                }
                rowBegin++;
                rowEnd--;
                colomnBegin++;
                colomnEnd--;
            }

            return ret;
        }
    };
