## AlgoExpert Searching Problems

### binary Search

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public static int binarySearch(int[] array, int target) {
    int l = 0 , r = array.length-1;
    while(l<=r){
      int mid = (l+r) / 2;
      if(array[mid] == target)
        return mid;
      else if(array[mid] > target)
        r = mid - 1;
      else
        l = mid + 1;
    }
    return -1;
  }
}
```

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
### find Three Largest Numbers

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int[] findThreeLargestNumbers(int[] array) {
        // Write your code here.
        
        int [] ans = new int[]{Integer.MIN_VALUE,Integer.MIN_VALUE,Integer.MIN_VALUE};
        for(int i=0;i<array.length;i++){
            if(ans[0]<array[i]){
                ans[2] = ans[1];
                ans[1] = ans[0];
                ans[0] = array[i];
            }else if(ans[1]<array[i]){
                ans[2] = ans[1];
                ans[1] = array[i];
            }else if(ans[2]<array[i]){
                ans[2] = array[i];
            }
        }
        return reverse(ans);
    }
    static int[] reverse(int a[])
    {
        int n = a.length;
        int[] b = new int[n];
        int j = n;
        for (int i = 0; i < n; i++) {
            b[j - 1] = a[i];
            j = j - 1;
        }
        return b;
    }
}
```
### shifted Binary Search

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int shiftedBinarySearch(int[] array, int target) {
        // Write your code here.
        int l=0,r=array.length-1;
        while(l<=r){
            int mid = (l+r)/2;
            if(array[mid] == target)
                return mid;
            if(array[l] <= array[mid]){
                if(target>=array[l] && target < array[mid])
                    r = mid-1;
                else
                    l = mid+1;
            }else{
                if(target<=array[r] && array[mid] < target)
                    l = mid+1;
                 else
                    r = mid-1;
            }
        }
        return -1;
    }
}

```
### quick select

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int quickselect(int[] array, int k) {
        // Write your code here.
        return quickselect(array,k-1,0,array.length-1);
    }

    private static int quickselect(int[] array, int k, int start, int end) {
        while (true) {
            if (start > end)
                throw new RuntimeException("Invalid Case");
            int pivot = start;
            int left = start + 1;
            int right = end;
            while (left <= right) {
                if (array[left] > array[pivot] && array[right] < array[pivot])
                    swap(left, right, array);
                if (array[left] < array[pivot])
                    left++;
                if (array[right] > array[pivot])
                    right--;
            }
            swap(right, pivot, array);
            if (right == k)
                return array[right];
            if (k > right)
                start = right + 1;
            else
                end = right - 1;
        }
    }

    private static void swap(int i, int j, int[] array) {
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
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
