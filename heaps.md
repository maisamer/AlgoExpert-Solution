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

### 

#### - JAVA Solution
```java
```

### 

#### - JAVA Solution
```java
```
### 
