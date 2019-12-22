# Leetcode 210
    class Solution {
    public:
        vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
            int size = prerequisites.size();
            vector<int> indegrees(numCourses, 0);
            vector<vector<int>> grid(numCourses, vector<int>()); //邻接数组，行数为numCourses


            for(int i = 0; i < size; i++){
                indegrees[prerequisites[i][0]]++;       //prerequisites[i][0]的入度
                grid[prerequisites[i][1]].push_back(prerequisites[i][0]); //以prerequisites[i][1]作为起始的邻接数组
            }

            queue<int> zeroIndegrees;
            for(int i = 0; i < numCourses; i++){//得到最开入度为0的课程编号，即先需要学习的课程
                if(indegrees[i] == 0){
                    zeroIndegrees.push(i);
                }
            }

            vector<int> ret;
            int count = 0;
            while(!zeroIndegrees.empty()){
                int front = zeroIndegrees.front();
                zeroIndegrees.pop();
                ret.push_back(front);
                count++;
                for(int i = 0; i < grid[front].size(); i++){//遍历front做为起始的邻接数组
                    indegrees[grid[front][i]]--;
                    if(indegrees[grid[front][i]] == 0){
                        zeroIndegrees.push(grid[front][i]);
                    }
                }
            }


            return count == numCourses ? ret : vector<int>();  //如果符合要求，则输出ret，否则输出[]
        }
    };
