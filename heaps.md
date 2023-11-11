## Heap problems solution

### Min Heap Construction

#### - JAVA Solution
```java
import java.util.*;

// Do not edit the class below except for the buildHeap,
// siftDown, siftUp, peek, remove, and insert methods.
// Feel free to add new properties and methods to the class.
class Program {
    static class MinHeap {
        List<Integer> heap = new ArrayList<Integer>();

        public MinHeap(List<Integer> array) {
            heap = buildHeap(array);
        }

        public List<Integer> buildHeap(List<Integer> array) {
            // Write your code here.
            int firstParentIdx = (array.size() - 2)/2;
            for(int currentIdx = firstParentIdx;currentIdx>=0;currentIdx--)
                siftDown(currentIdx,array.size()-1,array);
            return array;
        }

        public void siftDown(int currentIdx, int endIdx, List<Integer> heap) {
            // Write your code here.
            int childOneIdx = currentIdx*2 + 1;
            while(childOneIdx <= endIdx){
                int childTwoIdx = childOneIdx + 1;
                if(childTwoIdx > endIdx)
                    childTwoIdx = -1;
                if(childTwoIdx != -1 && heap.get(childTwoIdx) < heap.get(childOneIdx))
                    childOneIdx = childTwoIdx;
                if(heap.get(childOneIdx) < heap.get(currentIdx)){
                    swap(childOneIdx,currentIdx,heap);
                    currentIdx = childOneIdx;
                    childOneIdx = currentIdx*2 + 1;
                }else
                    break;
            }
        }

        private void swap(int i, int j, List<Integer> heap) {
            int temp = heap.get(i);
            heap.set(i,heap.get(j));
            heap.set(j,temp);
        }

        void siftUp(int currentIdx, List<Integer> heap) {
            int parentIdx = (currentIdx - 1)/2;
            while(currentIdx > 0 && heap.get(currentIdx) < heap.get(parentIdx)){
                swap(currentIdx,parentIdx,heap);
                currentIdx = parentIdx;
                parentIdx = (currentIdx - 1)/2;
            }
        }

        int peek() {
            return heap.isEmpty() ? -1 : heap.get(0);
        }

        int remove() {
            if(heap.isEmpty())
                return -1;
            int removedElement = heap.get(0);
            swap(0,heap.size()-1,heap);
            heap.remove(heap.size()-1);
            siftDown(0,heap.size()-1,heap);
            return removedElement;
        }

        void insert(int value) {
            heap.add(value);
            siftUp(heap.size()-1,heap);
        }
    }
}
```

### Continuous Median

#### - CPP Solution
```cpp
#include <cstdlib>
using namespace std;

// Do not edit the class below except for
// the insert method. Feel free to add new
// properties and methods to the class.
class ContinuousMedianHandler {
public:
  double median;
  priority_queue<int> maxHeap;
  priority_queue<int,vector<int>,greater<int>> minHeap;

  void insert(int number) {
    if(maxHeap.empty())
      maxHeap.push(number);
    else if(number >= maxHeap.top()){
      minHeap.push(number);
    }else{
      maxHeap.push(number);
    }
    if(maxHeap.size()-minHeap.size() == 2){
      int removedItem = maxHeap.top();
      maxHeap.pop();
      minHeap.push(removedItem);
    }else if(minHeap.size()-maxHeap.size() == 2){
      int removedItem = minHeap.top();
      minHeap.pop();
      maxHeap.push(removedItem);
    }
    if(maxHeap.size() == minHeap.size())
      median = (double)(minHeap.top()+maxHeap.top()) / 2;
    else if(maxHeap.size() > minHeap.size())
      median = maxHeap.top();
    else
      median = minHeap.top();
  }

  double getMedian() { 
    return median; 
  }
};
```

### sort K-Sorted Array

#### - CPP Solution
```cpp

#include <vector>
using namespace std;

vector<int> sortKSortedArray(vector<int> array, int k) {
  // Write your code here.
  if(array.empty() or !k)
    return array;
  if(k>=array.size())
    k = array.size()-1;

  priority_queue<int,vector<int>,greater<int>> minHeap;
  int index = 0;
  for(int i = 0;i<=k;i++){
    minHeap.push(array[i]);
  }
  for(int i = k+1;i<array.size();i++){
    array[index++] = minHeap.top();
    minHeap.pop();
    minHeap.push(array[i]);
  }
  while(!minHeap.empty()){
    array[index++] = minHeap.top();
    minHeap.pop();
  }
  return array;
}
```

### Laptop Rentals

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

int laptopRentals(vector<vector<int>> times) {
  sort(times.begin(),times.end());
  priority_queue<int,vector<int>,greater<int>> minHeap;
  for(auto interval:times){
    if(!minHeap.empty() and minHeap.top() <= interval[0])
        minHeap.pop();
    minHeap.push(interval[1]);
  }
  return minHeap.size();
}
```

### Merge Sorted Arrays

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static List<Integer> mergeSortedArrays(List<List<Integer>> arrays) {
        // Write your code here.
        List<PriorityQueue<Integer>> minHeap = new ArrayList<>();
        int sz = 0;
        for(List<Integer> list:arrays){
            minHeap.add(new PriorityQueue<>(list));
            sz+=list.size();
        }
        List<Integer> ans = new ArrayList<Integer>();
        while (sz>0){
            int ind = -1;
            int mn = Integer.MAX_VALUE;
            for(int i=0;i<arrays.size();i++){
                if(minHeap.get(i).isEmpty())
                    continue;
                if(mn>minHeap.get(i).peek()){
                    ind = i;
                    mn = minHeap.get(i).peek();
                }
            }
            ans.add(minHeap.get(ind).remove());
            sz--;
        }
        return ans;
    }
}
```

#### - another Solution
```java
import java.util.*;

class Program {
    public static List<Integer> mergeSortedArrays(List<List<Integer>> arrays) {
        // Write your code here.
        PriorityQueue<Item> minHeap = new PriorityQueue<>(Comparator.comparingInt(item -> item.value));
        for(int i=0;i<arrays.size();i++){
            minHeap.add(new Item(i,0,arrays.get(i).get(0)));
        }
        List<Integer> ans = new ArrayList<Integer>();
        while (!minHeap.isEmpty()){
            Item mnItem = minHeap.poll();
            ans.add(mnItem.value);
            if(arrays.get(mnItem.listInd).size()-1 == mnItem.itemInd)
                continue;
            minHeap.offer(new Item(mnItem.listInd, mnItem.itemInd+1,arrays.get(mnItem.listInd).get(mnItem.itemInd+1) ));
        }
        return ans;
    }

    private static class Item {
        int listInd;
        int itemInd;
        int value;

        public Item(int listInd, int itemInd, int value) {
            this.listInd = listInd;
            this.itemInd = itemInd;
            this.value = value;
        }
    }
}
```
