CC-2_Exp_1 (Karamveer Singh_24BDA70257)
class Solution { public: bool containsNearbyDuplicate(vector& nums, int k) { unordered_map<int, int> lastIndex;

    for (int i = 0; i < nums.size(); i++) {
        if (lastIndex.count(nums[i])) {
            if (i - lastIndex[nums[i]] <= k)
                return true;
        }
        lastIndex[nums[i]] = i;
    }

    return false;
}
};




CC-2_Exp_2 (Karamveer Singh_24BDA70257)
class Solution { public: vector productExceptSelf(vector& nums) { int n = nums.size(); vector answer(n, 1);

    int prefix = 1;
    for (int i = 0; i < n; i++) {
        answer[i] = prefix;
        prefix *= nums[i];
    }

    int suffix = 1;
    for (int i = n - 1; i >= 0; i--) {
        answer[i] *= suffix;
        suffix *= nums[i];
    }

    return answer;
}
};





CC-2_Exp_3 (Karamveer Singh _ 24BDA70257)
class Solution { public: int searchInsert(vector& nums, int target) { int left = 0, right = nums.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] == target)
            return mid;
        else if (nums[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }

    return left;
}
};




CC-2_Exp_4 (Karamveer Singh_24BDA70257)
class Solution { public: int search(vector& nums, int target) { int left = 0, right = nums.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] == target)
            return mid;

        if (nums[left] <= nums[mid]) {
            if (target >= nums[left] && target < nums[mid])
                right = mid - 1;
            else
                left = mid + 1;
        }
        else {
            if (target > nums[mid] && target <= nums[right])
                left = mid + 1;
            else
                right = mid - 1;
        }
    }

    return -1;
}
};




CC-2_Exp_5 (Karamveer Singh_24BDA70257)
class MyQueue { public: stack s1, s2;

MyQueue() {
}

void push(int x) {
    s1.push(x);
}

int pop() {
    if (s2.empty()) {
        while (!s1.empty()) {
            s2.push(s1.top());
            s1.pop();
        }
    }
    int val = s2.top();
    s2.pop();
    return val;
}

int peek() {
    if (s2.empty()) {
        while (!s1.empty()) {
            s2.push(s1.top());
            s1.pop();
        }
    }
    return s2.top();
}

bool empty() {
    return s1.empty() && s2.empty();
}
};

/**

Your MyQueue object will be instantiated and called as such:
MyQueue* obj = new MyQueue();
obj->push(x);
int param_2 = obj->pop();
int param_3 = obj->peek();
bool param_4 = obj->empty(); */





CC-2_Exp-6 (Karamveer Singh _ 24BDA70257)
class Solution { public: int largestRectangleArea(vector& heights) { stack st; heights.push_back(0); int maxArea = 0;

    for (int i = 0; i < heights.size(); i++) {
        while (!st.empty() && heights[st.top()] > heights[i]) {
            int h = heights[st.top()];
            st.pop();
            int w = st.empty() ? i : i - st.top() - 1;
            maxArea = max(maxArea, h * w);
        }
        st.push(i);
    }

    return maxArea;
}
};





CC-2_Exp-7 (Karamveer Singh _ 24BDA70257)
/**

Definition for singly-linked list.

struct ListNode {

int val;
ListNode *next;
ListNode() : val(0), next(nullptr) {}
ListNode(int x) : val(x), next(nullptr) {}
ListNode(int x, ListNode *next) : val(x), next(next) {}
}; / class Solution { public: bool isPalindrome(ListNode head) { if (!head || !head->next) return true;

 ListNode *slow = head, *fast = head;

 while (fast && fast->next) {
     slow = slow->next;
     fast = fast->next->next;
 }

 ListNode *prev = nullptr, *curr = slow;
 while (curr) {
     ListNode *next = curr->next;
     curr->next = prev;
     prev = curr;
     curr = next;
 }

 ListNode *first = head, *second = prev;
 while (second) {
     if (first->val != second->val)
         return false;
     first = first->next;
     second = second->next;
 }

 return true;
} };






CC-2_Exp-8 (Karamveer Singh _ 24BDA70257)
/**

Definition for singly-linked list.

struct ListNode {

int val;
ListNode *next;
ListNode() : val(0), next(nullptr) {}
ListNode(int x) : val(x), next(nullptr) {}
ListNode(int x, ListNode *next) : val(x), next(next) {}
}; / class Solution { public: ListNode oddEvenList(ListNode* head) { if (!head || !head->next) return head;

 ListNode* odd = head;
 ListNode* even = head->next;
 ListNode* evenHead = even;

 while (even && even->next) {
     odd->next = even->next;
     odd = odd->next;

     even->next = odd->next;
     even = even->next;
 }

 odd->next = evenHead;
 return head;
}

};
