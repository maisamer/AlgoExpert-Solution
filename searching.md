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
### 

#### - JAVA Solution
```java
```
