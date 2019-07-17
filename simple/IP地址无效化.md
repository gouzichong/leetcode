# Leetcode 1108
    class Solution {
    public:
        string defangIPaddr(string address) {
            int i;
            string ret;

            for(i = 0; i < address.size(); i++){
                if(address[i] == '.'){
                    ret += "[.]";
                }else{
                    ret.append(1, address[i]);
                }
            }

            return ret;
        }
    };
