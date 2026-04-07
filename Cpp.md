# Syntaxes

## 1. Remove duplicates from array
```cpp
ans.erase(unique(ans.begin(), ans.end()), ans.end());
```
### Explaination
- This arranges uniques at the start and return the pointer of the next.
```cpp
unique(ans.begin(), ans.end())
```
- [1,2,4,4,5,6,7,5,4]  ---> [1,2,4,5,6,7,4,5,4]
- erase removes from next pointer to end pointer
