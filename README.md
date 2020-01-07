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
``

## References :
https://www.programcreek.com/2013/01/leetcode-search-a-2d-matrix-java
