# Sorting
## Selection Sort

### Code
```cpp
class Solution {
public:
    vector<int> selectionSort(vector<int>& nums) {
       for(int i = 0; i < nums.size(); i++) {
        int mini = i;
        for(int j = i; j < nums.size(); j++) {
            if(nums[mini] > nums[j]) {
                mini = j;
            }
        }
        swap(nums[i], nums[mini]);
       }

       return nums;
    }
};
```
- Time Complexity : O(n^2)
- Select the smallest swap with the start of the window.

## Bubble Sort

### Code
```cpp
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        int n = nums.size();
        for (int i = n - 1; i > 0; i--) {
            int swaps = false;
            for (int j = 0; j < i; j++) {
                if (nums[j] > nums[j + 1]) {
                    swap(nums[j], nums[j + 1]);
                    swaps = true;
                }
            }

            if(!swaps) {
                break;
            }
        }
        return nums;
    }
};
```

- Time Complexity: O(n^2)
- Compare a pair in each step and swap if not in increasing order.
- Best time compexity will be O(n) if the array is sorted.

## Insertion Sort

### Code
```cpp
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        int n = nums.size();
        for(int i = 0; i < n; i++) {
            int j = i;
            while(j > 0 && nums[j] < nums[j-1]) {
                swap(nums[j], nums[j-1]);
                j--;
            }
        }

        return nums;
    }
};

```

- Time Complexity: O(n^2)
- Takes an element and places it in it's correct place(swap towards left till it can be).
- Best time complexity is O(n).