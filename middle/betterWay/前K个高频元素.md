# Leetcode 347
    class Solution {
    public:
        /*
        vector<int> topKFrequent(vector<int>& nums, int k) {
            int i;
            int j;
            unordered_map<int, int> con;
            unordered_map<int, int>::iterator iter;
            for(i = 0; i < nums.size(); i++){
                con[nums[i]]++;                                                         
            }

            map<int, vector<int>> countToNum;
            map<int, vector<int>>::reverse_iterator itr;
            for(iter = con.begin(); iter != con.end(); iter++){
                if(countToNum.find(iter->second) == countToNum.end()){
                    countToNum[iter->second] = vector<int>();
                }
                countToNum[iter->second].push_back(iter->first);
            }     

            vector<int> ret;
            int rank = 0;
            for(itr = countToNum.rbegin(); itr != countToNum.rend(); itr++){
                rank += itr->second.size();
                ret.insert(ret.end(), itr->second.begin(), itr->second.end());
                if(rank >= k){
                    break;
                }
            }

            return ret;
        }
        */

        //小根堆
        struct cmp{
            bool operator()(pair<int, int>& a, pair<int, int>& b){
                return a.second > b.second;
            }
        };

        vector<int> topKFrequent(vector<int>& nums, int k) {
            unordered_map<int, int> con;
            unordered_map<int, int>::iterator iter;
            for(int i = 0; i < nums.size(); i++){
                con[nums[i]]++;                                                         
            }

            priority_queue<pair<int, int>, vector<pair<int, int>>, cmp> pq;
            for(iter = con.begin(); iter != con.end(); iter++){
                pq.push(make_pair(iter->first, iter->second));
                if(pq.size() > k){
                    pq.pop();
                }
            }

            vector<int> ret;
            while(ret.size() < k){
                ret.push_back(pq.top().first);
                pq.pop();
            }


            return ret;
        }
    };
