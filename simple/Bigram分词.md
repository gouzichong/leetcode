# Leetcode 1078
    class Solution {
    public:
        vector<string> findOcurrences(string text, string first, string second) {
            string thirdStr, tmp = first + " " + second;
            int wordLen, offset = 0, len = tmp.length();
            vector<string> ret;

            //cout << text.length() << endl;
            while((offset = text.find(tmp, offset)) != string::npos){
                wordLen = 0;
                offset += len + 1;
                //cout << "offset is " << offset << endl;
                if(offset < text.length()){
                    while(text[offset] != ' ' && offset < text.length()){
                        wordLen++;
                        offset++;
                    }
                    offset -= wordLen;
                    //cout << "offset2 is " << offset << endl;
                    ret.push_back(text.substr(offset, wordLen));
                }
            }

            return ret;
        }
    };
