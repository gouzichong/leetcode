# Leetcode 535
    class Solution {
    public:

        // Encodes a URL to a shortened URL.
        string encode(string longUrl) {
            int length = longUrl.length();
            int i;

            string str;
            str.insert(0, longUrl, 0, 3);

            if(str == "ftp"){
                longUrl.erase(0, 3);
                longUrl.insert(0, "f");
            }
            else{
                longUrl.erase(0, 4);
                longUrl.insert(0, "h");
            }

            for(i = 0; i < length; i++){
                if(longUrl[i] == 'a')
                    longUrl[i] = 'A';
                else if(longUrl[i] == 'A')
                    longUrl[i] = 'a';

            }

            return longUrl;
        }

        // Decodes a shortened URL to its original URL.
        string decode(string shortUrl) {
            int length = shortUrl.length();
            int i;
            string add1 = "http";
            string add2 = "ftp";



            for(i = 0; i < length; i++){
                if(shortUrl[i] == 'A')
                    shortUrl[i] = 'a';
                else if(shortUrl[i] == 'a')
                    shortUrl[i] = 'A';
            }

            if(shortUrl[0] == 'h'){
                shortUrl.erase(0, 1);
                shortUrl.insert(0, add1);
            }
            if(shortUrl[0] == 'f'){
                shortUrl.erase(0, 1);
                shortUrl.insert(0, add2);
            }
            return shortUrl;
        }
    };

    // Your Solution object will be instantiated and called as such:
    // Solution solution;
    // solution.decode(solution.encode(url));
