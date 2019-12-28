# Leetcode 324
    class Solution {
    public:
        /*  //N*O(logN) and O(N)
        void wiggleSort(vector<int>& nums) {
            sort(nums.begin(), nums.end());
            vector<int>::iterator mid = nums.begin() + nums.size() / 2;
            if(nums.size() % 2){
                mid++;
            }

            vector<int> tmp1(nums.begin(), mid);
            vector<int> tmp2(mid, nums.end());

            //反序，穿插
            for(int i = 0; i < tmp1.size(); ++i){
                nums[2 * i] = tmp1[tmp1.size() - 1 - i];
            }
            for(int i = 0; i < tmp2.size(); ++i){
                nums[2 * i + 1] = tmp2[tmp2.size() - 1 - i];
            }
        }
        */


        //快速选择算法，找到中位数。不关心左右两边元素排列状况。但此时右边的一定大于中文数，左边小于等于中位数。O(N) and O(N)
        /*
        void quickSelect(vector<int>& nums, int begin, int end){
            int pivot = nums[end];
            int left = begin;
            int right = begin;
            while(right <= end){
                if(nums[right] <= pivot){
                    swap(nums[left++], nums[right++]);
                }else{             
                    ++right;
                }
            }
            left--;

            if(left < nums.size() / 2){
                quickSelect(nums, left+1, end);
            }else if(left > nums.size() / 2){
                quickSelect(nums, begin, left-1);
            }
        }
        */
        /* //way2
        //荷兰国旗，小于在左边，等于在中间，大于在右边
        void quickSelect(vector<int>& nums, int begin, int end){
            int pivot = nums[end];
            int left = begin;
            int i = begin;
            int right = end;
            while(i <= right){
                if(nums[i] > pivot){
                    swap(nums[i], nums[right--]);
                }else{
                    if(nums[i] < pivot){
                        swap(nums[i], nums[left++]);
                    }
                    i++;
                }
            }

            i--;
            if(i < nums.size() / 2){
                quickSelect(nums, i+1, end);
            }else if(i > nums.size() / 2){
                quickSelect(nums, begin, i-1);
            }
        }


        void wiggleSort(vector<int>& nums) {
            quickSelect(nums, 0, nums.size()-1);
            int midValue = nums[nums.size()/2];

            vector<int>::iterator mid = nums.begin() + nums.size() / 2;
            if(nums.size() % 2){
                mid++;
            }    

            vector<int> tmp1(nums.begin(), mid);
            vector<int> tmp2(mid, nums.end());

            //反序，穿插
            for(int i = 0; i < tmp1.size(); ++i){
                nums[2 * i] = tmp1[tmp1.size() - 1 - i];
            }
            for(int i = 0; i < tmp2.size(); ++i){
                nums[2 * i + 1] = tmp2[tmp2.size() - 1 - i];
            }  
        }   
        */


        //nth_element快速选择算法，找到中位数。两边都有可能有等于中位数 O(N) and O(1)
        void wiggleSort(vector<int>& nums) {
            int n = nums.size();

            auto midptr = nums.begin() + nums.size() / 2;
            nth_element(nums.begin(), midptr, nums.end());


            int midValue = *midptr;
            int left = 0;//奇位置
            int i = 0;
            int right = n - 1;//right是偶位置
            #define A(i) nums[(1 + 2*i) % (n | 1)]
            //nums数组的下标从[0, 1, 2, … , n - 1,] 映射到 [1, 3, 5, … , 0, 2, 4, …]得到数组A
            //在A中以中位数为界，将大于mid的元素排在中位数位置之前，将小于mid的元素排在中位数位置之后     
            //即实现左往右奇数索引位置放大于中位数的数, 然后从右往左在偶数索引位置放小于中位数的数，等于中位数则不变
            while(i <= right){
                if(A(i) > midValue){
                    swap(A(left++), A(i++));
                }else if(A(i) < midValue){
                    swap(A(i), A(right--));
                }else{
                    i++;
                }
            }
        }   

    };
