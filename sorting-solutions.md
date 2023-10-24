## AlgoExpert Sorting Problems

### Insertion Sort

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

vector<int> insertionSort(vector<int> array) {
  for(int i=1;i<array.size();i++){
    int j = i;
    while(j > 0 && array[j]<array[j-1]){
      swap(array[j],array[j-1]);
      j--;
    }
  }
  return array;
}
```
### Bubble Sort

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

vector<int> bubbleSort(vector<int> array) {
  // Write your code here.
  for(int i=0;i<array.size();i++)
    for(int j=i+1;j<array.size();j++)
      if(array[i]>array[j])
        swap(array[i],array[j]);
  return array;
}
```
### Selection Sort

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

vector<int> selectionSort(vector<int> array) {
  // Write your code here.
  for(int i=0;i<array.size()-1;i++){
    int smIndex = i;
    for(int j=i+1;j<array.size();j++){
      if(array[j]<array[smIndex])
        smIndex = j;
    }
    swap(array[i],array[smIndex]);
  }
  return array;
}
```
### three Number Sort

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public int[] threeNumberSort(int[] array, int[] order) {
        // Write your code here.
        Map<Integer,Integer> count = new HashMap<>();
        int index = 0;
        for (int j : array) {
            if (count.containsKey(j))
                count.put(j, count.get(j) + 1);
            else
                count.put(j, 1);
        }
        for(int o:order){
            if(!count.containsKey(o))
                continue;
            int size = count.get(o);
            for(int i=0;i<size;i++){
                array[index]=o;
                index++;
            }
        }
        return array;
    }
}
```
### quick Sort

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int[] quickSort(int[] array) {
        quickSort(array,0,array.length-1);
        return array;
    }
    public static void quickSort(int[] array,int startIdx,int endIdx) {
        if(startIdx >= endIdx)
            return;
        int pivot = startIdx;
        int left = startIdx+1;
        int right = endIdx;
        while(left <= right){
            if(array[left] > array[pivot] && array[right] < array[left])
                swap(left,right,array);
            if(array[left] <= array[pivot])
                left++;
            if(array[right] >= array[pivot])
                right--;
        }
        swap(pivot,right,array);
        boolean isLeftSmallerThan = right-1-startIdx < endIdx - (right+1);
        if(isLeftSmallerThan){
            quickSort(array,startIdx,right-1);
            quickSort(array,right+1,endIdx);
        }else{
            quickSort(array,right+1,endIdx);
            quickSort(array,startIdx,right-1);
        }
    }
    public static void swap(int i,int j,int []array){
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
}
```
### Heap Sort

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int[] heapSort(int[] array) {
        // Write your code here.
        buildMaxHeap(array);
        for(int end = array.length-1;end>0;end--){
            swap(0,end,array);
            siftDown(0,end-1,array);
        }
        return array;
    }

    private static void siftDown(int currentInd, int end, int[] array) {
        int childOne = currentInd*2+1;
        while (childOne<=end){
            int childTwo = currentInd*2+2;
            if(childTwo<=end && array[childTwo] > array[childOne])
                childOne = childTwo;
            if(array[childOne]>array[currentInd]){
                swap(currentInd,childOne,array);
                currentInd = childOne;
                childOne = currentInd*2+1;
            }else{
                return;
            }
        }
    }

    private static void swap(int i, int j, int[] array) {
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }

    private static void buildMaxHeap(int[] array) {
        int firstParentIdx = (array.length-2) / 2;
        for(int currentIdx = firstParentIdx;currentIdx>=0;currentIdx--){
            siftDown(currentIdx,array.length-1,array);
        }
    }

}
```
### Radix Sort 

#### - JAVA Solution
```java
import java.util.*;

class Program {

  public ArrayList<Integer> radixSort(ArrayList<Integer> array) {
    if(array.size() < 2)
      return array;
    int mx = Collections.max(array);
    int digit = 0;
    while(mx/(Math.pow(10,digit))>0){
      countingSort(array,digit);
      digit+=1;
    }
    return array;
  }
  public void countingSort(ArrayList<Integer> array,int digit){
    ArrayList<Integer> auxilirtyArray = new ArrayList<Integer>(Collections.nCopies(array.size(),0));
    ArrayList<Integer>  count = new ArrayList<Integer>(Collections.nCopies(11, 0));
    int digitColumn = (int) Math.pow(10,digit);
    for(Integer num : array){
      int index = (num / digitColumn) % 10;
      count.set(index,count.get(index)+1);
    }
    for(int i=1;i<10;i++){
      count.set(i,count.get(i) + count.get(i-1));
    }
    for(int i = array.size()-1;i>=0;i--){
      int index = (array.get(i) / digitColumn) % 10;
      int val = count.get(index) -1;
      count.set(index,val);
      auxilirtyArray.set(val , array.get(i));
    }
    for(int i = 0 ;i<array.size();i++)
      array.set(i , auxilirtyArray.get(i));
  }
  
}
```
### Merge Sort

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int[] mergeSort(int[] array) {
        // Write your code here.
        if(array.length <= 1)
            return array;
        int mid = array.length/2;
        int [] left = Arrays.copyOfRange(array,0,mid);
        int [] right = Arrays.copyOfRange(array,mid,array.length);
        return mergeSortedArrays(mergeSort(left),mergeSort(right));
    }

    private static int[] mergeSortedArrays(int[] left, int[] right) {
        int[] array = new int[left.length+right.length];
        int i = 0;
        int j = 0;
        int k = 0;
        while (i<left.length&&j<right.length)
            array[k++] = left[i] < right[j] ? left[i++]: right[j++];
        while(i<left.length)
            array[k++] = left[i++];
        while(j<right.length)
            array[k++] = right[j++];
        return array;
    }
}
```

#### - another Solution
```java
class Program {
    public static int[] mergeSort(int[] array) {
        // Write your code here.
        if(array.length <= 1)
            return array;
        int [] auxiliaryArray = array.clone();
        mergeSort(array,0,array.length-1,auxiliaryArray);
        return array;
    }

    private static void mergeSort(int[] mainArray, int start, int end, int[] auxiliaryArray) {
        if(start == end)
            return;
        int mid = (start+end) / 2;
        mergeSort(auxiliaryArray,start,mid,mainArray);
        mergeSort(auxiliaryArray,mid+1,end,mainArray);
        mergeSortedArrays(mainArray,start,mid,end,auxiliaryArray);
    }

    private static void mergeSortedArrays(int[] mainArray,
                                          int start, int mid, int end, int[] auxiliaryArray) {
        int i = start;
        int j = mid+1;
        int k = start;
        while(i<=mid&&j<=end)
            mainArray[k++] = auxiliaryArray[i] < auxiliaryArray[j] ? auxiliaryArray[i++]: auxiliaryArray[j++];
        while(i<=mid)
            mainArray[k++] = auxiliaryArray[i++];
        while(j<=end)
            mainArray[k++] = auxiliaryArray[j++];
    }
}
```

### Count Inversions

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public int countInversions(int[] array) {
        // Write your code here.
        return countSubArrayInversion(array,0,array.length);
    }

    private int countSubArrayInversion(int[] array, int start, int end) {
        if(end - start <= 1)
            return 0;
        int middle = start + (end - start) / 2;
        int leftInversions = countSubArrayInversion(array,start,middle);
        int rightInversions = countSubArrayInversion(array,middle,end);
        int mergedInversions = sortMergeInversions(array,start,middle,end);
        return leftInversions + rightInversions + mergedInversions;
    }

    private int sortMergeInversions(int[] array, int start, int middle, int end) {
        List<Integer> sortedArray = new ArrayList<>();
        int inversions = 0;
        int left = start;
        int right = middle;
        while (left<middle && right<end){
            if(array[left]<=array[right]){
                sortedArray.add(array[left]);
                left++;
            }else{
                sortedArray.add(array[right]);
                inversions+=middle-left;
                right++;
            }
        }
        while (left<middle){
            sortedArray.add(array[left]);
            left++;
        }
        while (right<end){
            sortedArray.add(array[right]);
            right++;
        }
        for(int i=0;i<sortedArray.size();i++)
            array[start+i] = sortedArray.get(i);
        return inversions;
    }
}
```
