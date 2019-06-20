# Leetcode 119
        class Solution {
        public:
            vector<int> getRow(int rowIndex) {
        /*
                vector<int> ret(rowIndex + 1, 1), tmp;
                int i, len = rowIndex;

                if(rowIndex < 2)
                    return ret;

                tmp = ret;
                rowIndex -= 1;
                while(rowIndex){
                    for(i = 1; i <= len - rowIndex; i++){
                        ret[i] = tmp[i] + tmp[i-1];
                    }
                    tmp = ret;
                    rowIndex--;
                }

                return ret;
        */

                vector<int> ret(rowIndex + 1, 1);
                int i, j;

                for(i = 2; i <= rowIndex; i++){
                    for(j = i - 1; j > 0; j--){
                        ret[j] += ret[j - 1];
                    }
                }

                return ret;
            }
        };
