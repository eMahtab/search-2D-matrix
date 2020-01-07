# Search 2D Matrix
## https://leetcode.com/problems/search-a-2d-matrix

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.
```
Example 1:

Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
Output: true

Example 2:

Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
Output: false
```

## Approach :
There are lot of hints in this question, and its clearly telling us to use binary search as the elements in the 2D matrix are sorted.
e.g. element at matrix[3][4] is guaranteed to be greater than or equal to element at matrix[3][3], since elements in each row are sorted in ascending order.

So we can solve this problem by running binary search over each row of the 2D matrix, one by one. However the time complexity of this approach will be O(m * log(n)), where m is the number of rows in the input matrix and n is the number of columns in the input matrix.

### Can we do better : ❓

❗️ Note that we are given that the first element of next row will be greater than the last element of the current row. 

So basically we can treat the entire 2D matrix as a sorted 1D matrix and perform a binary search. 
The time complexity of this approach will be O(log(m * n)) , where m is the number of rows in the input matrix and n is the number of columns in the input matrix, which is much better than O(m * log(n)) 😊

Below example shows that log(m * n) is much better than n * log(m)
```
n = 8 (number of rows)
m = 8 (number of columns)
n * log(m) = 8 * log(8) = 8 * 3 = 24
log(m * n) = log(8 * 8) = log(64) = 6

```
### Coding the second approach : 

The start index will be 0 and end index will be `m * n - 1`

```java
int start = 0;
int end = m * n - 1; // <-- m is number of rows and n is number of columns

```
Now the most important thing is, how we find the row and column for the element at `mid`.
If we look carefully, we can see that, for mid element row will be `(mid / n)` and column will be `(mid % n)`

```java
int mid = (start + end) / 2;
int row = mid / n;
int column = mid % n;
```

## Implementation : 

```java
public static boolean searchMatrix(int[][] matrix, int target) {
      if(matrix == null || matrix.length == 0)
        return false;  
        
      int m = matrix.length;
      int n = matrix[0].length;

      int start = 0;
      int end = m * n - 1;
       
      while(start <= end){
         int mid = (start + end) / 2;
         int row = mid / n;
         int column = mid % n;
          
         if(matrix[row][column] > target){
           end = mid - 1;
         } else if(matrix[row][column] < target){
           start = mid + 1;
         } else{
           return true;
         }
      }
        
    return false;
  }
```
Above implementation have runtime complexity of O(log(m * n)) and space complexity of O(1), where m is the number of rows in the input matrix and n is the number of columns in the input matrix.

```
Runtime Complexity = O(log(m * n))
Space Complexity   = O(1)
```

## References :
1. https://www.youtube.com/watch?v=dHJDhsvBd8c
2. https://www.programcreek.com/2013/01/leetcode-search-a-2d-matrix-java
