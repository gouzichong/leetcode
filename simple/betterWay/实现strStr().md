# Leetcode 28
      class Solution {
      public:
          //kmp to get next, next[i] = k(k>0) represent needle[i-1] = needle[k-1]
          void getNext(const string& p, vector<int> &next){
              int i = 0;
              int j = -1;
              next[0] = -1;

              while(i < p.size()){
                  if(j == -1 || p[i] == p[j]){
                      ++i;
                      ++j;
                      next[i] = j;
                  }else{
                      j = next[j];
                  }
              }
          }


          int strStr(string haystack, string needle) {
              //kmp
              int i;
              int j;
              int nSize = needle.size();
              vector<int> next(needle.size() + 1);

              getNext(needle, next);
      /*       
              for(i = 0; i < next.size(); i++){
                  cout << next[i] << " ";
              }
      */       
              i = 0;
              j = 0;
              while(i < haystack.size() && j < nSize){  // nSize can't replace by needle.size(), because need.size() is unsigned int, when compare with -1, -1 will convert to unsigned int.
                  if(j == -1 || haystack[i] == needle[j]){
                      ++i;
                      ++j;
                  }else{
                      j = next[j];
                  }
              }

              if(j == needle.size()){
                  return i-j;
              }

              return -1;




      /*
              if(needle.size() == 0){
                  return 0;
              }

              if(needle.size() > haystack.size() || (needle.size() == haystack.size() && needle != haystack)){
                  return -1;
              }

              int i, j;


              for(i = 0; i <= haystack.size() - needle.size(); i++){
                  j = 0;
                  while(j < needle.size() && haystack[i] == needle[j]){
                      j++; 
                      i++;
                  }

                  if(j == needle.size()){
                      return i - j; 
                  }

                  if(j != 0){
                      i = i - j;
                  }
              }

              return -1; 
      */

      /*        
              if(needle.size() == 0){
                  return 0;
              }

              if(needle.size() > haystack.size() || (needle.size() == haystack.size() && needle != haystack)){
                  return -1;
              }

              int i, j;

              j = 0;
              for(i = 0; i < haystack.size(); i++){
                  if(i + needle.size() - j > haystack.size()){
                      return -1;
                  }
                  if(haystack[i] == needle[j]){
                      if(j == needle.size() - 1){
                          return i - j;
                      }
                      j++;
                  }else{
                      i -= j;
                      j = 0;
                  }
              }

              return -1; 
      */
          }
      };
