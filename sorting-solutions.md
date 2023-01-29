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
### Two Number Sum

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
