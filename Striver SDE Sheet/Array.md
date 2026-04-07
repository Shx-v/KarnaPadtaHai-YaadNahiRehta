# Array I

## Set Matrix Zeros

- [LeetCode](https://leetcode.com/problems/set-matrix-zeroes/)

```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        bool firstRowZero = false;
        bool firstColZero = false;

        int rows = matrix.size();
        int cols = matrix[0].size();

        for(int i = 0; i < cols; i++) {
            if(matrix[0][i] == 0) firstRowZero = true;
        }

        for(int j = 0; j < rows; j++) {
            if(matrix[j][0] == 0) firstColZero = true;
        }

        for(int i = 1; i < rows; i++) {
            for(int j = 1; j < cols; j++) {
                if(matrix[i][j] == 0) {
                    matrix[0][j] = 0;
                    matrix[i][0] = 0;
                }
            }
        }

        for(int i = 1; i < rows; i++) {
            for(int j = 1; j < cols; j++) {
                if(matrix[0][j] == 0 || matrix[i][0] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        if(firstRowZero) {
            for(int i = 0; i < cols; i++) {
                matrix[0][i] = 0;
            }
        }

        if(firstColZero) {
            for(int i = 0; i < rows; i++) {
                matrix[i][0] = 0;
            }
        }
    }
};
```

## Pascal's Triangle 1

- [LeetCode](https://leetcode.com/problems/pascals-triangle/)

```cpp
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> ans;

        for (int i = 0; i < numRows; i++) {
            ans.push_back(vector<int>(i + 1, 1));
        }

        for (int i = 2; i < numRows; i++) {
            for (int j = 1; j < i; j++) {
                ans[i][j] = ans[i - 1][j - 1] + ans[i - 1][j];
            }
        }

        return ans;
    }
};
```

## Next Permutation

- [LeetCode](https://leetcode.com/problems/next-permutation/)

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int n = nums.size();
        int ptr = -1;

        for (int i = n - 1; i > 0; i--) {
            if (nums[i - 1] < nums[i]) {
                ptr = i - 1;
                break;
            }
        }

        if (ptr != -1) {
            int minIdx = ptr + 1;
            for (int i = ptr + 1; i < n; i++) {
                if (nums[i] > nums[ptr] && nums[i] <= nums[minIdx]) {
                    minIdx = i;
                }
            }
            swap(nums[ptr], nums[minIdx]);
        }

        reverse(nums.begin() + ptr + 1, nums.end());
    }
};
```

## Kadane's Algorithm

- [LeetCode](https://leetcode.com/problems/maximum-subarray/)

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int sum = nums[0], maxSum = nums[0];

        for(int i = 1; i < nums.size(); i++) {
            if(sum < 0) sum = 0;
            sum += nums[i];

            maxSum = max(sum, maxSum);
        }

        return maxSum;
    }
};
```

## Sort an Array of 0's 1's and 2's

- [LeetCode](https://leetcode.com/problems/sort-colors/)

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int low = 0,mid = 0, high = nums.size() - 1;

        while(mid <= high) {
            if(nums[mid] == 0) {
                swap(nums[mid], nums[low]);
                mid++;
                low++;
            } else if(nums[mid] == 2) {
                swap(nums[mid], nums[high]);
                high--;
            } else if(nums[mid] == 1) {
                mid++;
            }
        }
    }
};
```
## Stock Buy and Sell

- [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock)

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int minPrice = INT_MAX;
        int maxProfit = 0;

        for(auto it:prices) {
            minPrice = min(minPrice, it);
            int profit = it-minPrice;
            maxProfit = max(maxProfit, profit);
        }
        return maxProfit;
    }
};
```