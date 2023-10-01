## AlgoExpert Searching Problems

### search In Sorted Matrix

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

vector<int> searchInSortedMatrix(vector<vector<int>> matrix, int target) {
  int n = matrix.size(), m = matrix[0].size()-1;
  int row = 0,col = m;
  while(row < n and col >= 0){
    if(matrix[row][col]>target)
      col--;
    else if(matrix[row][col]<target)
      row++;
    else
      return {row,col};
  }
  return {-1,-1};
}
```
### search For Range

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int[] searchForRange(int[] array, int target) {
        // Write your code here.
        int[] result = new int[] {-1, -1};
        getRangeValues(array,result,target,true);
        getRangeValues(array,result,target,false);
        return result;
    }

    private static void getRangeValues(int[] array, int[] result, int target,boolean leftDirection) {
        int l=0, r=array.length-1;
        while(l<=r){
            int mid = (l+r)/2;
            if(array[mid] == target) {
                if(leftDirection){
                    if(mid == 0 || array[mid-1] != target){
                        result[0] = mid;
                        return;
                    }else{
                        r = mid -1;
                    }
                }else {
                    if(mid == array.length-1 || array[mid+1] != target){
                        result[1] = mid;
                        return;
                    }else{
                        l = mid +1;
                    } 
                }
            }
            else if(array[mid] > target)
                r = mid -1;
            else
                l = mid +1;
        }
    }


}
```
### 

#### - JAVA Solution
```java
```
### 

#### - JAVA Solution
```java
```
### 

#### - JAVA Solution
```java
```
### 

#### - JAVA Solution
```java
```
### 

#### - JAVA Solution
```java
```
### 

#### - JAVA Solution
```java
```
### 

#### - JAVA Solution
```java
```
### 

#### - JAVA Solution
```java
```
### 

#### - JAVA Solution
```java
```
