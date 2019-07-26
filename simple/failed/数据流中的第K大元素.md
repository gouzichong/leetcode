# Leetcode 703
    class KthLargest {
    public:
        KthLargest(int k, vector<int>& nums) {
            kVal = k;
            for(int i = 0; i < nums.size(); i++){
                container.push(nums[i]);
                if(container.size() > kVal){
                    container.pop();
                }
            }
        }

        int add(int val) {
            container.push(val);
            if(container.size() > kVal){
                container.pop();
            }
            return container.top();
        }
    private:
        priority_queue<int, vector<int>, greater<int>> container;
        int kVal;
    };

    /**
     * Your KthLargest object will be instantiated and called as such:
     * KthLargest* obj = new KthLargest(k, nums);
     * int param_1 = obj->add(val);
     */
