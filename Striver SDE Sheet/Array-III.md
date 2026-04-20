# Array III

## Search in a 2D matrix

- [LeetCode](https://leetcode.com/problems/search-a-2d-matrix/)

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size(), n = matrix[0].size();
        int low = 0, high = m*n - 1;

        while(low <= high) {
            int mid = low + (high - low) / 2;

            int indX = mid/n;
            int indY = mid%n;

            if(matrix[indX][indY] == target) {
                return true;
            } else if(matrix[indX][indY] > target) {
                high = mid-1;
            } else {
                low = mid+1;
            }
        }

        return false;
    }
};
```

## Pow(x,n)

- [LeetCode](https://leetcode.com/problems/powx-n/)

```cpp
class Solution {
public:
    double myPow(double x, int n) {
        long long N = n;

        if (N < 0) {
            x = 1 / x;
            N = -N;
        }

        return power(x, N);
    };

    double power(double x, long long n) {
        if (n == 0) return 1;

        double half = power(x, n / 2);

        if (n % 2 == 0) {
            return half * half;
        } else {
            return half * half * x;
        }
    }
};
```

## Majority Element I

- [LeetCode](https://leetcode.com/problems/majority-element/)

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int current = nums[0], cnt = 0;

        for (auto it : nums) {
            if (current == it) {
                cnt++;
            } else {
                if (cnt == 0) {
                    current = it;
                    cnt = 1;
                } else {
                    cnt--;
                }
            }
        }

        return current;
    }
};
```

## Majority Element II

- [LeetCode](https://leetcode.com/problems/majority-element-ii)

```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        int n = nums.size();
        int curr1 = 0, curr2 = 0;
        int cnt1 = 0, cnt2 = 0;

        if (n == 0)
            return {};

        for (int it : nums) {
            if (curr1 == it) {
                cnt1++;
            } else if (curr2 == it) {
                cnt2++;
            } else if (cnt1 == 0) {
                curr1 = it;
                cnt1 = 1;
            } else if (cnt2 == 0) {
                curr2 = it;
                cnt2 = 1;
            } else {
                cnt1--;
                cnt2--;
            }
        }

        cnt1 = cnt2 = 0;

        for (int it : nums) {
            if (it == curr1) {
                cnt1++;
            } else if (it == curr2) {
                cnt2++;
            }
        }

        vector<int> ans;

        if (cnt1 > n / 3)
            ans.push_back(curr1);
        if (cnt2 > n / 3)
            ans.push_back(curr2);

        return ans;
    }
};
```

## Grid Unique Paths

- [LeetCode](https://leetcode.com/problems/unique-paths/)

### Recursion
```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        int row = 0, col = 0;
        int ways = 0;

        solve(row, col, m, n, ways);

        return ways;
    }

    void solve(int row, int col, int m, int n, int& ways) {
        if (row == m - 1 && col == n - 1) {
            ways++;
            return;
        }
        
        if(row < m-1) solve(row + 1, col, m, n, ways);
        if(col < n-1) solve(row, col + 1, m, n, ways);
    }
};
```

### DP
```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m, vector<int>(n, -1));
        
        return solve(0,0,m,n,dp);
    }

    int solve(int row, int col, int m, int n, vector<vector<int>>& dp) {
        if (row == m - 1 && col == n - 1) {
            return 1;
        }

        if(dp[row][col] != -1) return dp[row][col];
        
        int ways = 0;
        
        if(row < m-1) ways += solve(row+1, col, m, n, dp);
        if(col < n-1) ways += solve(row, col+1, m, n, dp);

        return dp[row][col] = ways;
    }
};
```

### DP wih Space Optimization
```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<int> dp(n, 1);

        for (int i = m - 2; i >= 0; i--) {
            for (int j = n - 2; j >= 0; j--) {
                dp[j] = dp[j] + dp[j + 1];
            }
        }

        return dp[0];
    }
};
```

## Reverse Pairs

- [LeetCode](https://leetcode.com/problems/reverse-pairs/)

```cpp
class Solution {
public:
    int countPairs(vector<int>& arr, int low, int mid, int high) {
        int count = 0, right = mid + 1;
        for (int i = low; i <= mid; i++) {
            while (right <= high && (long long)arr[i] > 2LL * arr[right])
                right++;

            count = count + (right - (mid + 1));
        }
        return count;
    }

    void merge(vector<int>& arr, int left, int mid, int right) {

        int n1 = mid - left + 1;
        int n2 = right - mid;

        vector<int> L(n1), R(n2);

        for (int i = 0; i < n1; i++)
            L[i] = arr[left + i];
        for (int j = 0; j < n2; j++)
            R[j] = arr[mid + 1 + j];

        int i = 0, j = 0;
        int k = left;

        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k] = L[i];
                i++;
            } else {
                arr[k] = R[j];
                j++;
            }
            k++;
        }

        while (i < n1) {
            arr[k] = L[i];
            i++;
            k++;
        }

        while (j < n2) {
            arr[k] = R[j];
            j++;
            k++;
        }
    }

    int mergeSort(vector<int>& arr, int left, int right) {
        int count = 0;
        if (left >= right)
            return count;

        int mid = left + (right - left) / 2;
        count += mergeSort(arr, left, mid);
        count += mergeSort(arr, mid + 1, right);
        count += countPairs(arr, left, mid, right);
        merge(arr, left, mid, right);

        return count;
    }
    int reversePairs(vector<int>& arr) {
        int n = arr.size();
        return mergeSort(arr, 0, n - 1);
    }
};
```
