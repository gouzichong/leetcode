# Leetcode 378
    class Solution {
    public:
        /*
        int kthSmallest(vector<vector<int>>& matrix, int k) {
            priority_queue<int, vector<int>, less<int>> con; //大根堆

            int size = matrix.size();
            for(int i = 0; i < size; i++){
                for(int j = 0; j < size; j++){
                    if(con.size() == k){
                        if(matrix[i][j] > con.top()){
                            continue;
                        }else{
                            con.pop();
                        }
                    }
                    con.push(matrix[i][j]);

                }
            }

            return con.top();
        }
        */

        int kthSmallest(vector<vector<int>>& matrix, int k) {
            int size = matrix.size();
            int begin = matrix[0][0];
            int end = matrix[size-1][size-1];

            while(begin < end){
                int mid = begin + (end - begin) / 2;
                int count = 0;  //小于mid的数
                int j = size - 1;

                for(int i = 0; i < size; i++){
                    while(j >= 0 && matrix[i][j] > mid){
                        j--;
                    }
                    count += j + 1;
                }

                if(count < k){
                    begin = mid + 1;
                }else{
                    end = mid;
                }

            }

            return begin;
        }
    };
