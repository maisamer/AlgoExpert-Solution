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
### Youngest Common Ancestor

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

class AncestralTree {
public:
  char name;
  AncestralTree *ancestor;

  AncestralTree(char name) {
    this->name = name;
    this->ancestor = nullptr;
  }

  void addAsAncestor(vector<AncestralTree *> descendants);
};
int getDepth(AncestralTree *root,AncestralTree *node){
  if(node->name == root->name)
    return 0;
  return 1 + getDepth(root,node->ancestor);
}

AncestralTree *getYoungestCommonAncestor(AncestralTree *topAncestor,
                                         AncestralTree *descendantOne,
                                         AncestralTree *descendantTwo) {
  int d1 = getDepth(topAncestor,descendantOne);
  int d2 = getDepth(topAncestor,descendantTwo);
  if(d1 > d2){
    int steps = d1 - d2;
    while(steps--){
      descendantOne = descendantOne->ancestor;
    }
  }else{
    int steps = d2 - d1;
    while(steps--){
      descendantTwo = descendantTwo->ancestor;
    }
  }
  while(descendantOne->name != descendantTwo->name){
    descendantTwo = descendantTwo->ancestor;
    descendantOne = descendantOne->ancestor;
  }
  return descendantTwo;
}
```
### Youngest Common Ancestor another approach 

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

class AncestralTree {
public:
  char name;
  AncestralTree *ancestor;

  AncestralTree(char name) {
    this->name = name;
    this->ancestor = nullptr;
  }

  void addAsAncestor(vector<AncestralTree *> descendants);
};

AncestralTree *getYoungestCommonAncestor(AncestralTree *node,
                                         AncestralTree *descendantOne,
                                         AncestralTree *descendantTwo) {
  unordered_set<char> visited;
  while(descendantOne){
    visited.insert(descendantOne->name);
    descendantOne = descendantOne->ancestor;
  }
  while(descendantTwo){
    if(visited.find(descendantTwo->name) != visited.end())
      return descendantTwo;
    descendantTwo = descendantTwo->ancestor;
  }
  return nullptr;
}
```
### Remove Islands

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
bool valid(int x,int y,int n,int m){
  return x>=0 and y>=0 and x<n and y<m;
}
void updateArea(vector<vector<int>> &matrix,int x,int y,int value,int n,int m){
  if(!valid(x,y,n,m) or matrix[x][y] != 1)
    return ;
  matrix[x][y] = value;
  updateArea(matrix,x+1,y,value,n,m);
  updateArea(matrix,x,y+1,value,n,m);
  updateArea(matrix,x-1,y,value,n,m);
  updateArea(matrix,x,y-1,value,n,m);
}
vector<vector<int>> removeIslands(vector<vector<int>> matrix) {
  int n = matrix.size();
  int m = matrix[0].size();
  for(int i=0;i<n;i++){
    if(matrix[i][0] == 1)
      updateArea(matrix,i,0,2,n,m);
    if(matrix[i][m-1] == 1)
      updateArea(matrix,i,m-1,2,n,m);
  }
  for(int i=0;i<m;i++){
    if(matrix[0][i] == 1)
      updateArea(matrix,0,i,2,n,m);
    if(matrix[n-1][i] == 1)
      updateArea(matrix,n-1,i,2,n,m);
  }
  for(int i=1;i<n-1;i++)
    for(int j=1;j<m-1;j++)
      if(matrix[i][j] == 1)
        updateArea(matrix,i,j,0,n,m);
        
  for(int i=0;i<n;i++)
    for(int j=0;j<m;j++)
      if(matrix[i][j] == 2)
        matrix[i][j] = 1;
  
  return matrix;
}
```
### cycle In Graph

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public boolean cycleInGraph(int[][] edges) {
        // Write your code here.
        Set<Integer> vis = new HashSet<>();
        Set<Integer> inStack = new HashSet<>();
        for(int i=0;i<edges.length;i++){
            if(!vis.contains(i)){
                if(hasCycle(i,edges,vis,inStack))
                    return true;
            }
        }
        return false;
    }

    private boolean hasCycle(int vertex, int[][] edges, Set<Integer> vis, Set<Integer> inStack) {
        vis.add(vertex);
        inStack.add(vertex);
        for(int i=0;i<edges[vertex].length;i++){
            if(!vis.contains(edges[vertex][i])){
                if(hasCycle(edges[vertex][i],edges,vis,inStack))
                    return true;
            }else{
                if(inStack.contains(edges[vertex][i]))
                    return true;
            }
        }
        inStack.remove(vertex);
        return false;
    }
}
```
### minimum Passes Of Matrix

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public int minimumPassesOfMatrix(int[][] matrix) {
        // Write your code here.
        Queue<List<Integer>> q = new LinkedList<>();
        int[] dx = new int[]{1,-1,0,0};
        int[] dy = new int[]{0,0,1,-1};
        int passes = 0;
        int height = matrix.length;
        int width = matrix[0].length;
        for(int i=0;i<height;i++)
            for(int j=0;j<width;j++)
                if(matrix[i][j] > 0)
                    q.add(List.of(i,j));
        while(!q.isEmpty()){
            int sz = q.size();
            boolean countPass = false;
            while (sz>0){
                List<Integer> point = q.remove();
                for(int i=0;i<4;i++){
                    int x = point.get(0)+dx[i];
                    int y = point.get(1)+dy[i];
                    if(valid(x,y,height,width) && matrix[x][y] < 0) {
                        if(!countPass){
                          passes++;
                          countPass = true;
                        }
                        q.add(List.of(x, y));
                        matrix[x][y] *=-1;
                    }
                }
                sz--;
            }
        }
        for (int[] ints : matrix)
            for (int anInt : ints)
                if (anInt < 0)
                    return -1;
        return passes;
    }

    private boolean valid(int x, int y, int height, int width) {
        return x<height && x>=0 && y<width && y>=0;
    }
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
