## AlgoExpert Graph Problems

### Depth First Search

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
class Node {
public:
  string name;
  vector<Node *> children;

  Node(string str) { name = str; }

  vector<string> depthFirstSearch(vector<string> *array) {
    Node *node = this;
    array->push_back(node->name);
    for(auto child : node->children)
      child->depthFirstSearch(array);
    return *array;
  }
  Node *addChild(string name) {
    Node *child = new Node(name);
    children.push_back(child);
    return this;
  }
};
```
### Single Cycle Check

#### - CPP Solution
```cpp
using namespace std;

bool hasSingleCycle(vector<int> array) {
  int n = array.size();
  int cnt = n;
  int index = 0;
  while(cnt >= 0){
    if(cnt == 0 and index == 0)
      return true;
    else if((cnt != n and index == 0) or (cnt == 0 and index != 0))
      return false;
    cnt--;
    int step = array[index];
    index = (index + step) % n;
    index = index>=0 ? index : index+n;
  }
  return false;
}
```
### Breadth First Search

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

class Node {
public:
  string name;
  vector<Node *> children;

  Node(string str) { name = str; }

  vector<string> breadthFirstSearch(vector<string> *array) {
    queue<Node *> q;
    q.push(this);
    while(!q.empty()){
      int sz = q.size();
      while(sz--){
        Node *curr = q.front();
        array->push_back(curr->name);
        q.pop();
        for(auto child : curr->children)
          q.push(child);
      }
    }
    return *array;
  }

  Node *addChild(string name) {
    Node *child = new Node(name);
    children.push_back(child);
    return this;
  }
};
```
### River Sizes

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
bool valid(int x,int y,int n,int m){
  return x>=0 and y>=0 and x<n and y<m;
}
int getRiverSize(vector<vector<int>> &matrix,int startX,int startY) {
  if(!valid(startX,startY,matrix.size(),matrix[0].size()) or !matrix[startX][startY])
    return 0;
  matrix[startX][startY] = 0;
  return 1 + getRiverSize(matrix,startX+1,startY)+
  getRiverSize(matrix,startX,startY+1)+
  getRiverSize(matrix,startX-1,startY)+
  getRiverSize(matrix,startX,startY-1);
}
vector<int> riverSizes(vector<vector<int>> matrix) {
  vector<int> ans;
  for(int i=0;i<matrix.size();i++){
    for(int j=0;j<matrix[i].size();j++){
      if(matrix[i][j])
        ans.push_back(getRiverSize(matrix,i,j));
    }
  }
  return ans;
}
```
### 

#### - CPP Solution
```cpp
```
### 

#### - CPP Solution
```cpp
```
### 

#### - CPP Solution
```cpp
```
### 

#### - CPP Solution
```cpp
```
### 

#### - CPP Solution
```cpp
```
### 

#### - CPP Solution
```cpp
```
### 

#### - CPP Solution
```cpp
```
