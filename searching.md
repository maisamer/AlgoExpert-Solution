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
### Index Equals Value

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public int indexEqualsValue(int[] array) {
        // Write your code here.
        int l = 0, r = array.length-1;
        int ans = -1;
        while(l<=r){
            int mid = (l+r)/2;
            if(mid == array[mid]){
                ans = mid;
                r = mid - 1;
            }else if(mid < array[mid]){
                r = mid - 1;
            }else{
                l = mid + 1;
            }
        }
        return ans;
    }
}
```
### median Of Two Sorted Arrays

#### - JAVA Solution
```java
import java.util.*;

class Program {
    // O(log(min(m,n))) time | O(1) space
    public float medianOfTwoSortedArrays(int[] arrayOne, int[] arrayTwo) {
        // Write your code here.
        int [] big = arrayOne.length >= arrayTwo.length ? arrayOne : arrayTwo;
        int [] small = arrayOne.length < arrayTwo.length ? arrayOne : arrayTwo;
        int l = 0,r = small.length-1;
        int mergedPartIdx = (big.length+small.length-1) / 2;
        while (true){
            int smallerIdx = (int) Math.floor((double)(l+r)/2);
            int bigIdx = mergedPartIdx - smallerIdx - 1;
            int mxLeftSmall = smallerIdx>=0 ? small[smallerIdx]:Integer.MIN_VALUE;
            int mnRightSmall = smallerIdx+1 < small.length ? small[smallerIdx+1]:Integer.MAX_VALUE;
            int mxLeftBig = bigIdx>=0 ? big[bigIdx]:Integer.MIN_VALUE;
            int mnRightBig = bigIdx+1 < big.length ? big[bigIdx+1]:Integer.MAX_VALUE;
            if(mnRightBig < mxLeftSmall)
                r = smallerIdx -1;
            else if(mxLeftBig > mnRightSmall)
                l = smallerIdx + 1;
            else{
                if((arrayOne.length+arrayTwo.length)%2 == 0){
                    return (float)(Math.max(mxLeftBig,mxLeftSmall) + Math.min(mnRightSmall,mnRightBig))/2;
                }
                return Math.max(mxLeftBig,mxLeftSmall);
            }
        }
    }
}
```

#### - another Solution
```java
import java.util.*;

class Program {
    //O(n+m) time | O(1) space 
    public float medianOfTwoSortedArrays(int[] arrayOne, int[] arrayTwo) {
        // Write your code here.
        int len = arrayOne.length+arrayTwo.length;
        int mid = len/2;
        int i1 = 0;
        int i2 = 0;
        float ans = 0;
        Integer num1 = null,num2 = null;
        while (mid>0){
            if(i1 < arrayOne.length && i2 < arrayTwo.length){
                if(arrayOne[i1] < arrayTwo[i2]) {
                    num1 = arrayOne[i1];
                    i1++;
                }else if (arrayOne[i1] == arrayTwo[i2]){
                    if(i1+1 >= arrayOne.length || arrayOne[i1+1] >= arrayTwo[i2+1]) {
                        num1 = arrayTwo[i2];
                        i2++;
                    } else if(i2+1 >= arrayTwo.length || arrayOne[i1+1] < arrayTwo[i2+1]){
                        num1 = arrayOne[i1];
                        i1++;
                    }
                }
                else {
                    num1 = arrayTwo[i2];
                    i2++;
                }
            }else if(i1 < arrayOne.length) {
                num1 = arrayOne[i1];
                i1++;
            }else {
                num1 = arrayTwo[i2];
                i2++;
            }
            mid--;
        }
        if(i1 < arrayOne.length && i2 < arrayTwo.length){
            num2 =  Math.min(arrayOne[i1], arrayTwo[i2]);
        }else if(i1 < arrayOne.length)
            num2 = arrayOne[i1];
        else
            num2 = arrayTwo[i2];
        return len%2 == 0?  (float) (num2+num1)/2:num2;
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

