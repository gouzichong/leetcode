# Leetcode 1103
    class Solution {
    public:
        vector<int> distributeCandies(int candies, int num_people) {
    /*
            vector<int> ret;
            int i, cur = 1;

            ret.resize(num_people);

            i = 0;
            while(candies > 0){
                ret[i] += cur < candies ? cur : candies;
                candies -= cur;
                cur++;
                i++;
                if(ret.size() == i)
                    i = 0;
            }

            return ret;
    */


            int i, time = 0, remain = 0;
            vector<int> ret;

            ret.resize(num_people);
            remain = candies;

            while(1){
                candies -= num_people * (2 * time * num_people + 1 + num_people) / 2;
                if(candies > 0){
                    time++;
                    remain = candies;
                }else
                    break;
            }
            time--;


            for(i = 0; i < ret.size(); i++){
                ret[i] = num_people * (time * (time + 1)) / 2 + (time + 1) * (i + 1);
                if(remain > 0){
                    ret[i] += min(((time + 1) * num_people + i + 1), remain);
                    remain -= ((time + 1) * num_people + i + 1);
                }
            }

            return ret;

        }
    };
