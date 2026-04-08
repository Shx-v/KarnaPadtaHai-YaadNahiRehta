# Arrary II

## Rotate Matrix by 90 Degrees

- [LeetCode](https://leetcode.com/problems/rotate-image/)

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        for(int i = 0; i < matrix.size(); i++) {
            for(int j = i+1; j < matrix[0].size(); j++) {
                swap(matrix[i][j], matrix[j][i]);
            }

            reverse(matrix[i].begin(), matrix[i].end());
        }
    }
};
```

## Merge Two Overlapping Subintervals

- [LeetCode](https://leetcode.com/problems/merge-intervals/)

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        vector<vector<int>> ans;

        sort(intervals.begin(), intervals.end());
        
        for (auto& interval : intervals) {
            if (ans.empty() || ans.back()[1] < interval[0]) {
                ans.push_back(interval);
            } else {
                ans.back()[1] = max(ans.back()[1], interval[1]);
            }
        }

        return ans;
    }
};
```

## Merge Two Sorted Arrays without extra space

- [LeetCode](https://leetcode.com/problems/merge-sorted-array/)

```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = m - 1;
        int j = n - 1;
        int k = m + n - 1;

        while (i >= 0 && j >= 0) {
            if (nums1[i] > nums2[j]) {
                nums1[k--] = nums1[i--];
            } else {
                nums1[k--] = nums2[j--];
            }
        }

        while (j >= 0) {
            nums1[k--] = nums2[j--];
        }
    }
};
```

## Find Duplicate Number

- [LeetCode](https://leetcode.com/problems/find-the-duplicate-number/)

```cpp
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow = nums[0];
        int fast = nums[0];
        
        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while(slow != fast);
        
        slow = nums[0];
        
        while(slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }
        
        return slow;
    }
};
```

## Find the Repeating and Missing number

- [GfG](https://www.geeksforgeeks.org/problems/find-missing-and-repeating2512/1)

```cpp
class Solution {
  public:
    vector<int> findTwoElement(vector<int>& arr) {
        int n = arr.size();
        int dup = -1;
        long long miss = 0;
        
        for (int it : arr) {
            int val = abs(it);
            
            miss += val;
            
            if (arr[val - 1] < 0 && dup == -1) {
                dup = val;
            }
            
            if (arr[val - 1] > 0) {
                arr[val - 1] = -arr[val - 1];
            }
        }
        
        miss = (1LL * n * (n + 1)) / 2 - miss + dup;
        
        return {dup, (int)miss};
    }
};
```

- [LeetCode](https://leetcode.com/problems/find-missing-and-repeated-values)

```cpp
class Solution {
public:
    vector<int> findMissingAndRepeatedValues(vector<vector<int>>& grid) {
        int n = grid.size();
        int dup = -1;
        long long miss = 0;

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                int val = abs(grid[i][j]);

                miss += val;

                int indI = (val - 1) / n;
                int indJ = (val - 1) % n;

                if (grid[indI][indJ] < 0 && dup == -1) {
                    dup = val;
                }

                if (grid[indI][indJ] > 0) {
                    grid[indI][indJ] = -grid[indI][indJ];
                }
            }
        }

        miss = (1LL * (n * n) * ((n * n) + 1)) / 2 - miss + dup;

        return {dup, (int)miss};
    }
};
```

## Count Inversions

- [GfG](https://www.geeksforgeeks.org/problems/inversion-of-array-1587115620/1)

```cpp
class Solution {
  public:
    int inversionCount(vector<int> &arr) {
        // Code Here
        int cnt = 0;
        mergeSort(arr, 0, arr.size() - 1, cnt);

        return cnt;
    }
    
    void merge(vector<int>& nums, int low, int mid, int high, int& cnt) {
        vector<int> temp;
        int i = low, j = mid + 1;

        while (i <= mid && j <= high) {
            if (nums[i] <= nums[j]) {
                temp.push_back(nums[i]);
                i++;
            } else {
                temp.push_back(nums[j]);
                j++;
                cnt += (mid - i + 1);
            }
        }

        while (i <= mid) {
            temp.push_back(nums[i]);
            i++;
        }
        while (j <= high) {
            temp.push_back(nums[j]);
            j++;
        }

        for (int k = low; k <= high; k++) {
            nums[k] = temp[k - low];
        }
    }

    void mergeSort(vector<int>& nums, int low, int high, int& cnt) {
        if (low >= high) return;

        int mid = low + (high - low) / 2;

        mergeSort(nums, low, mid, cnt);
        mergeSort(nums, mid + 1, high, cnt);

        merge(nums, low, mid, high, cnt);
    }
};
```
