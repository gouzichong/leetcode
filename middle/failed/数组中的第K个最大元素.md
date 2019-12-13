# Leetcode 215
    class Solution {
    public:
        /*
        int findKthLargest(vector<int>& nums, int k) {
            sort(nums.begin(), nums.end());
            return nums[nums.size() - k];
        }
        */

    /*   //借鉴快速排序的方法
        int partition(vector<int>& nums, int left, int right)
        {
            int pivot = left + rand() % (right - left);
            swap(nums[pivot], nums[right]);  //枢纽放到right位置
            int j = right - 1;
            int i = left;


            while(i <= j){  //区间为1时i==j也要进入循环，因为后面return前做了swap
                if(nums[i] < nums[right]){
                    swap(nums[i], nums[j--]);  //小于枢纽值的放在右边
                    continue;
                }
                i++;
            }

            swap(nums[i], nums[right]);
            return i;
        }

        int findKthLargest(vector<int>& nums, int k) {
            int left = 0;
            int right = nums.size() - 1;

            k--;
            while(left < right){
                int index = partition(nums, left, right);         
                if(index == k){
                    return nums[index];
                }
                if(index < k){
                    left = index + 1;
                }else{
                    right = index - 1;
                }
            }

            return nums[right];
        }
    */
        //建立k大小的小根堆


        void heapInsert(vector<int> &arr, int size, int data){
            arr[size] = data;
            int childIndex = size;
            int parentIndex = (childIndex - 1) / 2;

            //shiftUp
            while(parentIndex >= 0){
                if(arr[childIndex] < arr[parentIndex]){
                    swap(arr[childIndex], arr[parentIndex]);
                    childIndex = parentIndex;
                    parentIndex = (childIndex - 1) / 2;
                }else{
                    break;
                }
            }
        }

        void shiftDown(vector<int> &arr, int size, int newData){
            arr[0] = newData;
            int parentIndex = 0;
            int leftIndex = 2 * parentIndex + 1;

            while(leftIndex < size){
                int minIndex = leftIndex + 1 < size && arr[leftIndex+1] < arr[leftIndex] ? leftIndex + 1 : leftIndex;
                minIndex = arr[minIndex] < arr[parentIndex] ? minIndex : parentIndex;
                if(parentIndex == minIndex){
                    break;
                }
                swap(arr[parentIndex], arr[minIndex]); 
                parentIndex = minIndex;
                leftIndex = parentIndex * 2 + 1;
            }
        }


        int findKthLargest(vector<int>& nums, int k) {
            vector<int> minHeap(k);
            for(int i = 0; i < k; i++){
                heapInsert(minHeap, i, nums[i]);
            }


            for(int i = k; i < nums.size(); i++){
                if(nums[i] > minHeap[0]){
                    shiftDown(minHeap, k, nums[i]);
                }
            }

            return minHeap[0];
        }
    };
