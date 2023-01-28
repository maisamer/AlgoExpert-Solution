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
### 

#### - CPP Solution
```cpp
```
