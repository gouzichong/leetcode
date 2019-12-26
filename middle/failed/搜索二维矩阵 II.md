# Leetcode 240
    class Solution {
    public:
        /*
        //双指针O(N+M)
        bool searchMatrix(vector<vector<int>>& matrix, int target) {
            if(matrix.size() == 0 || matrix[0].size() == 0){
                return false;
            }
            int row = matrix.size() - 1; 
            int column = 0;
            while(row >= 0 && column < matrix[0].size()){ //从左下角向上判断
                if(matrix[row][column] == target){
                    return true;
                }else if(matrix[row][column] > target){
                    row--;
                }else{
                    column++;
                }
            }

            return false;
        }
        */
        /*分冶
        bool dfs(vector<vector<int>> &matrix, int &target, int rowBegin, int rowEnd, int columnBegin, int columnEnd){
            if(rowBegin > rowEnd || columnBegin > columnEnd){
                return false;
            }

            int min = matrix[rowBegin][columnBegin]; //左上角
            int max = matrix[rowEnd][columnEnd];  //右下角
            if(min > target || max < target){
                return false;
            }
            if(min == target || max == target){
                return true;
            }

            int columnMid = (columnBegin + columnEnd) / 2;

            int row = rowBegin;
            while (row <= rowEnd && matrix[row][columnMid] <= target) { //判断中间的一列
                if (matrix[row][columnMid] == target) {
                    return true;
                }
                row++;
            }
            //此时  matrix[row-1][columnEnd] < target < matrix[row][columnMid]

            //只用判断左下和右上两个区域
            return dfs(matrix, target, row, rowEnd, columnBegin, columnMid-1) 
                || dfs(matrix, target, rowBegin, row-1, columnMid+1, columnEnd);
        }

        bool searchMatrix(vector<vector<int>>& matrix, int target) {
            if(matrix.size() == 0 || matrix[0].size() == 0){
                return false;
            }

            return dfs(matrix, target, 0, matrix.size()-1, 0, matrix[0].size()-1);
        }  
        */

        //二分法
        bool searchBinary(vector<vector<int>> &matrix, int &target, int start, bool scanRow){
            int begin = start;
            int end = scanRow ? matrix[0].size() - 1 : matrix.size() - 1;

            while(begin <= end){
                int mid = begin + (end - begin) / 2;
                if(scanRow){
                    if(matrix[start][mid] == target){
                        return true;
                    }else if(matrix[start][mid] > target){
                        end = mid - 1;
                    }else{
                        begin = mid + 1;
                    }
                }else{
                    if(matrix[mid][start] == target){
                        return true;
                    }else if(matrix[mid][start] > target){
                        end = mid - 1;
                    }else{
                        begin = mid + 1;
                    }
                }
            }
            return false;
        }

        bool searchMatrix(vector<vector<int>>& matrix, int target) {
            if(matrix.size() == 0 || matrix[0].size() == 0){
                return false;
            }
            int minD = min(matrix.size(), matrix[0].size());
            for(int i = 0; i < minD; i++){
                int ret = searchBinary(matrix, target, i, true);//横着扫描
                if(ret){
                    return true;
                }
                ret = searchBinary(matrix, target, i, false);  //竖着扫描
                if(ret){
                    return true;
                }
            }

            return false;
        }  
    };
