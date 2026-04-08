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