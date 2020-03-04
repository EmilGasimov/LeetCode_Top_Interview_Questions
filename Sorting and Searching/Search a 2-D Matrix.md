Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.

### Solution [own]
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix == null || matrix.length == 0 || matrix[0].length == 0) return false;
        int rows = matrix.length, cols = matrix[0].length;
        return helper(matrix, 0, rows - 1, 0, cols - 1, target);
    }
    
    private boolean helper(int[][] matrix, int topRow, int bottomRow, int leftCol, int rightCol, 
                           int target) {
        if(topRow > bottomRow || leftCol > rightCol) return false;
        
        if(topRow == bottomRow) {
            return binarySearch(matrix[topRow], leftCol, rightCol, target);
        }
        
        if(leftCol == rightCol) {
            while(topRow < bottomRow) {
                if(matrix[(topRow + bottomRow)/2][leftCol] == target) return true;
                if(matrix[(topRow + bottomRow)/2][leftCol] > target) {
                    bottomRow = (topRow + bottomRow)/2 - 1;
                }
                else topRow = (topRow + bottomRow)/2 + 1;
            }
            if(topRow == bottomRow && matrix[topRow][leftCol] == target) return true;
            return false;
        }
        
        int midRow = (topRow + bottomRow)/2, midCol = (leftCol + rightCol)/2;
        if(target == matrix[midRow][midCol]) return true;
        if(target > matrix[midRow][midCol]) {
            return  helper(matrix, midRow + 1, bottomRow, leftCol, rightCol, target) ||
                    helper(matrix, topRow, midRow, midCol + 1, rightCol, target);
                                            
        }
        return  helper(matrix, topRow, bottomRow, leftCol, midCol - 1, target) ||
                helper(matrix, topRow, midRow - 1, midCol, rightCol, target);        
    }
    
    private boolean binarySearch(int[] nums, int start, int end, int target) {
        if(start > end) return false;
        if(start == end) return nums[start] == target;
        if(nums[(start + end)/2] == target) return true;
        if(nums[(start + end)/2] > target) 
            return binarySearch(nums, start, (start + end)/2 - 1, target);
        return binarySearch(nums, (start + end)/2 + 1, end, target);
    }
}
```
### Solution [efficient; time complexity : O(number of rows + number of columsn)]
```java
public boolean searchMatrix(int[][] matrix, int target) {
    if (matrix == null || matrix.length == 0 || matrix[0].length == 0)
        return false;

    int n = matrix.length, m = matrix[0].length;
    int i = 0, j = m - 1;
    
    while (i < n && j >= 0) {
        int num = matrix[i][j];
        
        if (num == target)
            return true;
        else if (num > target)
            j--;
        else
            i++;
    }
    
    return false;
}
```
