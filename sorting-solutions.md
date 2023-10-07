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
### Two Number Sum

#### - CPP Solution
```cpp

```
### 

#### - CPP Solution
```cpp

```
### Two Number Sum

#### - CPP Solution
```cpp

```
### Two Number Sum

#### - CPP Solution
```cpp

```
