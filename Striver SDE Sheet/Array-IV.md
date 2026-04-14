# Array IV

## Two Sum

- [LeetCode](https://leetcode.com/problems/two-sum/)

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> mp;

        for(int i =0; i < nums.size(); i++) {
            int comp = target - nums[i];

            if(mp.find(comp) != mp.end()) {
                return {mp[comp], i};
            }

            mp[nums[i]] = i;
        }

        return {};
    }
};
```

## Three Sum

- [LeetCode](https://leetcode.com/problems/3sum)

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> ans;
        sort(nums.begin(), nums.end());

        for (int i = 0; i < nums.size(); i++) {
            if (i != 0 && nums[i] == nums[i - 1])
                continue;

            int j = i + 1;
            int k = nums.size() - 1;

            while (j < k) {
                int sum = nums[i] + nums[j] + nums[k];
                if (sum < 0) {
                    j++;
                } else if (sum > 0) {
                    k--;
                } else {
                    ans.push_back({nums[i], nums[j], nums[k]});
                    j++;
                    k--;
                    while (j < k && nums[j] == nums[j - 1])
                        j++;
                    while (j < k && nums[k] == nums[k + 1])
                        k--;
                }
            }
        }

        return ans;
    }
};
```

## Four Sum

- [LeetCode](https://leetcode.com/problems/4sum/)

```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());

        vector<vector<int>> ans;

        for(int i = 0; i < nums.size(); i++) {
            if(i != 0 && nums[i] == nums[i-1]) continue;

            for(int j = i+1; j < nums.size(); j++) {
                if(j > i+1 && nums[j] == nums[j-1]) continue;

                int k = j + 1;
                int l = nums.size() - 1;

                while(k < l) {
                    long long sum = (long long)nums[i] + nums[j] + nums[k] + nums[l];

                    if(sum < target) {
                        k++;
                    } else if(sum > target) {
                        l--;
                    } else {
                        ans.push_back({nums[i], nums[j], nums[k], nums[l]});
                        k++;
                        l--;
                        while(k < l && nums[k] == nums[k-1]) k++;
                        while(k < l && nums[l] == nums[l+1]) l--;
                    }
                }
            }
        }

        return ans;
    }
};
```

## Longest Consequtive Sequence in an Array

- [LeetCode](https://leetcode.com/problems/longest-consecutive-sequence/)

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> st(nums.begin(), nums.end());
        int longest = 0;

        for(auto it: st) {
            if(st.find(it-1) == st.end()) {
                int curr = it;
                int cnt = 1;

                while(st.find(curr + 1) != st.end()){
                    cnt++;
                    curr++;
                }

                longest = max(longest, cnt);
            }
        }

        return longest;
    }
};
```