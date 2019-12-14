# Leetcode 146
    class LRUCache {
    public:
        /*
        LRUCache(int capacity) {
            capacity_ = capacity;
        }

        int get(int key) {
            auto pos = container_.find(key);
            if(pos != container_.end()){
                int value = pos->second->second;
                list_.erase(pos->second);
                list_.push_front(make_pair(key, value));
                container_[key] = list_.begin();
                return value;
            }
            return -1;
        }

        void put(int key, int value) {
            auto pos = container_.find(key);
            if(pos != container_.end()){
                list_.erase(pos->second);
            }
            list_.push_front(make_pair(key, value));
            if(list_.size() > capacity_){
                int key = list_.back().first;
                container_.erase(key);
                list_.pop_back();
            }
            container_[key] = list_.begin();
        }

        unordered_map<int, list<pair<int, int>>::iterator> container_;
        list<pair<int, int>> list_;
        int capacity_;
        */

        struct Node
        {
            int key_;
            int value_;
            Node *prev;
            Node *next;
            Node(int key, int value)
                : key_(key), value_(value)
            {
                prev = NULL;
                next = NULL;
            }
        };

        void moveToHead(Node *node){
            if(head == NULL){
                head = node;
                tail = node;
                node->prev = NULL;
                node->next = NULL;
                return;
            }

            node->next = head;
            head->prev = node;
            node->prev = NULL;
            head = node;
        }

        void deleteNode(Node *node){
            if(node != head){
                node->prev->next = node->next;
            }

            if(node != tail){
                node->next->prev = node->prev;
            }

            if(node == head){
                head = node->next;
            }

            if(node == tail){
                tail = node->prev;
            }
        }


        LRUCache(int capacity) {
            capacity_ = capacity;
            head = NULL;
            tail = NULL;
        }


        int get(int key) {
            auto pos = container_.find(key);
            if(pos != container_.end()){
                deleteNode(pos->second);
                moveToHead(pos->second);
                container_[key] = pos->second;
                return pos->second->value_;
            }
            return -1;
        }

        void put(int key, int value) {
            auto pos = container_.find(key);
            if(pos != container_.end()){
                deleteNode(pos->second);
            }else{
                if(container_.size() == capacity_){
                    container_.erase(tail->key_);
                    deleteNode(tail);
                }
            }

            Node *newNode = new Node(key, value);
            moveToHead(newNode);
            container_[key] = newNode;
        }

        unordered_map<int, Node*> container_;
        Node *head;
        Node *tail;
        int capacity_;
    };

    /**
     * Your LRUCache object will be instantiated and called as such:
     * LRUCache* obj = new LRUCache(capacity);
     * int param_1 = obj->get(key);
     * obj->put(key,value);
     */
