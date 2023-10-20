## BST problems solution

### find Closest Value In Bst

#### - CPP Solution
```cpp
class BST {
public:
  int value;
  BST *left;
  BST *right;

  BST(int val);
  BST &insert(int val);
};
int findClosestValueInBstHelper(BST *tree, int target,int &close) {
  if(tree == nullptr)
    return close;
  if(close == INT_MAX ||  abs(close-target) > abs(target-tree->value))
    close = tree->value;
  if(target < tree->value)
    return findClosestValueInBstHelper(tree->left,target,close);
  else if(target > tree->value)
    return findClosestValueInBstHelper(tree->right,target,close);
  else
    return close;
}

int findClosestValueInBst(BST *tree, int target) {
  int close = INT_MAX;
  return findClosestValueInBstHelper(tree,target,close);
}
```

### BST Construction

#### - JAVA Solution
```java
import java.util.*;

class Program {
  static class BST {
    public int value;
    public BST left;
    public BST right;

    public BST(int value) {
      this.value = value;
    }

    private BST insert(BST node,int value){
      if(node == null)
        return new BST(value);
      if(value >= node.value)
        node.right = insert(node.right,value);
      else
        node.left = insert(node.left,value);
      return node;
    }

    public BST insert(int value) {
      // Write your code here.
      // Do not edit the return statement of this method.
      insert(this,value);
      return this;
    }

    private boolean contains(BST node,int value){
      if(node == null)
        return false;
      if(node.value == value)
        return true;
      if(value >= node.value)
        return contains(node.right,value);
      return contains(node.left,value);
    }

    public boolean contains(int value) {
      // Write your code here.
      return contains(this,value);
    }
    private int getMin(){
      if(left == null)
        return value;
      else
        return left.getMin();
    }
    private void remove(int value,BST parent){
      BST currentNode = this;
      while(currentNode != null){
        if(value > currentNode.value){
          parent = currentNode;
          currentNode = currentNode.right;
        }else if(value < currentNode.value){
          parent = currentNode;
          currentNode = currentNode.left;
        }else{
          if(currentNode.left != null && currentNode.right != null){
            currentNode.value = currentNode.right.getMin();
            //System.out.println("min value is "+currentNode.value);
            currentNode.right.remove(currentNode.value,currentNode);
          }else if(parent == null){
            if(currentNode.left != null){
              currentNode.value = currentNode.left.value;
              currentNode.right = currentNode.left.right;
              currentNode.left = currentNode.left.left;
            }else if(currentNode.right != null){
              currentNode.value = currentNode.right.value;
              currentNode.left = currentNode.right.left;
              currentNode.right = currentNode.right.right;
            }else{
              
            }
          }else if(parent.left == currentNode){
            parent.left = currentNode.left != null ? currentNode.left:currentNode.right;
          }else if(parent.right == currentNode){
            parent.right = currentNode.left != null ? currentNode.left:currentNode.right;
          }
          break;
        }
      }
    }

    public BST remove(int value) {
      // Write your code here.
      // Do not edit the return statement of this method.
      remove(value,null);
      return this;
    }
  }
}
```
### validate Bst

#### - CPP Solution
```cpp
class BST {
public:
  int value;
  BST *left;
  BST *right;

  BST(int val);
  BST &insert(int val);
};

bool validateBstHelper(BST *tree,int lower,int upper) {
  if(tree == nullptr)
    return true;

  if(tree->value >= upper or tree->value < lower)
    return false;
  
  return validateBstHelper(tree->left,lower,tree->value) and 
          validateBstHelper(tree->right,tree->value,upper);
}

bool validateBst(BST *tree) {
  return validateBstHelper(tree,INT_MIN,INT_MAX);
}
```

### BST Traverse

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

class BST {
public:
  int value;
  BST *left;
  BST *right;

  BST(int val);
};

void inOrderTraverse(BST *tree, vector<int> &array) {
  if(tree == nullptr)
    return;
  inOrderTraverse(tree->left,array);
  array.push_back(tree->value);
  inOrderTraverse(tree->right,array);
}

void preOrderTraverse(BST *tree, vector<int> &array) {
  if(tree == nullptr)
    return;
  array.push_back(tree->value);
  preOrderTraverse(tree->left,array);
  preOrderTraverse(tree->right,array);
}

void postOrderTraverse(BST *tree, vector<int> &array) {
  // Write your code here.
    if(tree == nullptr)
    return;
  postOrderTraverse(tree->left,array);
  postOrderTraverse(tree->right,array);
  array.push_back(tree->value);
}
```
### min Height Bst

#### - CPP Solution
```cpp
using namespace std;

class BST {
public:
  int value;
  BST *left;
  BST *right;

  BST(int value) {
    this->value = value;
    left = nullptr;
    right = nullptr;
  }

  void insert(int value) {
    if (value < this->value) {
      if (left == nullptr) {
        left = new BST(value);
      } else {
        left->insert(value);
      }
    } else {
      if (right == nullptr) {
        right = new BST(value);
      } else {
        right->insert(value);
      }
    }
  }
};

BST *minHeightBst(vector<int> array,BST*bst,int l,int r) {
  if(l>r)
    return nullptr;
  int mid = (l+r)/2;
  int rootValue = array[mid];
  if(bst == nullptr)
    bst = new BST(rootValue);
  else
    bst->insert(rootValue);
  minHeightBst(array,bst,l,mid-1); 
  minHeightBst(array,bst,mid+1,r); 
  return bst;
}

BST *minHeightBst(vector<int> array) {
  return minHeightBst(array,nullptr,0,array.size()-1);
}
```

### find Kth Largest Value In Bst

#### - CPP Solution
```cpp
using namespace std;

// This is an input class. Do not edit.
class BST {
public:
  int value;
  BST *left = nullptr;
  BST *right = nullptr;

  BST(int value) { this->value = value; }
};
class TreeInfo{
public:
  int numVisited = 0;
  int lastValue = -1;
};

void findKthLargestValueInBst(BST *node,int k,TreeInfo &treeInfo) {
  if(node == nullptr or k == 0)
    return;
  findKthLargestValueInBst(node->right,k,treeInfo);
  if(treeInfo.numVisited < k){
    treeInfo.numVisited +=1;
    treeInfo.lastValue = node->value;
    findKthLargestValueInBst(node->left,k,treeInfo); 
  }
}
int findKthLargestValueInBst(BST *node,int k) {
  TreeInfo treeInfo;
  findKthLargestValueInBst(node,k,treeInfo);
  return treeInfo.lastValue;
}
```
### reconstruct Bst

#### - CPP Solution
```cpp
using namespace std;

// This is an input class. Do not edit.
class BST {
public:
  int value;
  BST *left = nullptr;
  BST *right = nullptr;

  BST(int value) { this->value = value; }
};

BST *reconstructBst(vector<int> preOrderTraversalValues) {
  if(preOrderTraversalValues.empty())
    return nullptr;
  BST *root = new BST(preOrderTraversalValues[0]);
  int rightIndex = preOrderTraversalValues.size();
  for(int i=1;i<preOrderTraversalValues.size();i++){
    if(preOrderTraversalValues[i]>=preOrderTraversalValues[0]){
      rightIndex = i;
      break;
    }
  }
  root->left = reconstructBst(vector<int>(preOrderTraversalValues.begin()+1,
                              preOrderTraversalValues.begin()+rightIndex));
  root->right = reconstructBst(vector<int>(preOrderTraversalValues.begin() + rightIndex,
                              preOrderTraversalValues.end()));

  return root;
}
```

### same Bsts

#### - CPP Solution
```cpp
#include <vector>

using namespace std;

bool sameBsts(vector<int> a, vector<int> b) {
  if(a.empty() && b.empty())
    return true;
  if(a.size() != b.size() || a[0] != b[0])
    return false;
  vector<int> al,ar,bl,br;
  for(int i=1;i<a.size();i++){
    if(a[0]>a[i]){
      al.push_back(a[i]);
    }else{
      ar.push_back(a[i]);
    }
    if(b[0]>b[i]){
      bl.push_back(b[i]);
    }else{
      br.push_back(b[i]);
    }
  }
  
  return sameBsts(al,bl) && sameBsts(ar,br);
}
```
### validate Three Nodes

#### - JAVA Solution
```java
import java.util.*;

class Program {
  // This is an input class. Do not edit.
  static class BST {
    public int value;
    public BST left = null;
    public BST right = null;

    public BST(int value) {
      this.value = value;
    }
  }

  public boolean search(BST parent,BST child){
    if(parent == null)
      return false;
    if(child.value == parent.value)
      return true;
    if(child.value > parent.value)
      return search(parent.right,child);
    return search(parent.left,child);
  }

  public boolean validateThreeNodes(BST nodeOne, BST nodeTwo, BST nodeThree) {
    // Write your code here.
    if(search(nodeOne,nodeTwo)){
      if(search(nodeTwo,nodeThree))
        return true;
    }else if(search(nodeThree,nodeTwo)){
      if(search(nodeTwo,nodeOne))
        return true;
    }
    return false;
  }
}
```

#### - another Solution
```java
import java.util.*;

class Program {
  // This is an input class. Do not edit.
  static class BST {
    public int value;
    public BST left = null;
    public BST right = null;

    public BST(int value) {
      this.value = value;
    }
  }

  public boolean isAncestor(BST parent,BST child){
    BST current = parent;
    while(current != null){
      if(child.value == current.value)
        return true;
      if(child.value > current.value)
        current = current.right;
      else
        current = current.left; 
    }
    return false;
  }

  public boolean validateThreeNodes(BST nodeOne, BST nodeTwo, BST nodeThree) {
    // Write your code here.
    if(search(nodeOne,nodeTwo))
      return search(nodeTwo,nodeThree);
    else if(search(nodeThree,nodeTwo))
      return search(nodeTwo,nodeOne);
    return false;
  }
}
```

#### - another Solution
```java
import java.util.*;

class Program {
  // This is an input class. Do not edit.
  static class BST {
    public int value;
    public BST left = null;
    public BST right = null;

    public BST(int value) {
      this.value = value;
    }
  }

  public boolean isAncestor(BST parent,BST child){
    BST current = parent;
    while(current != null){
      if(child.value == current.value)
        return true;
      if(child.value > current.value)
        current = current.right;
      else
        current = current.left; 
    }
    return false;
  }

  public boolean validateThreeNodes(BST nodeOne, BST nodeTwo, BST nodeThree) {
    BST solutionOne = nodeOne, solutionTwo = nodeThree;
    while(true){
      boolean foundThreeFromOne = solutionOne == nodeThree;
      boolean foundOneFromThree = solutionTwo == nodeOne;
      boolean foundNodeTwo = solutionOne == nodeTwo || solutionTwo == nodeTwo;
      boolean finishedSearching = solutionOne == null && solutionTwo == null;
      if(foundThreeFromOne || foundOneFromThree || foundNodeTwo ||finishedSearching)
        break;
      if(solutionOne != null)
        solutionOne = solutionOne.value < nodeTwo.value ? solutionOne.right : solutionOne.left;
      if(solutionTwo != null)
        solutionTwo = solutionTwo.value < nodeTwo.value ? solutionTwo.right : solutionTwo.left;
    }
    if(solutionOne == nodeThree || solutionTwo == nodeOne || !(solutionOne == nodeTwo || solutionTwo == nodeTwo))
     return false; 
    
    if(solutionOne == nodeTwo)
      return isAncestor(nodeTwo,nodeThree);

     return isAncestor(nodeTwo,nodeOne);
  }
}
```
### repair Bst

#### - JAVA Solution
```java
import java.util.*;

class Program {
  // This is an input class. Do not edit.
  static class BST {
    public int value;
    public BST left = null;
    public BST right = null;

    public BST(int value) {
      this.value = value;
    }
  }
  BST nodeOne,nodeTwo,prevNode;
  public BST repairBst(BST tree) {
    // Write your code here.
    inorderTraverse(tree);
    int temp = nodeOne.value;
    nodeOne.value = nodeTwo.value;
    nodeTwo.value = temp;
    return tree;
  }
  void inorderTraverse(BST node){
    if(node == null)
      return;
    inorderTraverse(node.left);
    // visit the node
    if(prevNode != null && node.value < prevNode.value){
      if(nodeOne == null)
        nodeOne = prevNode;
      nodeTwo = node;
    }
    prevNode = node;
    inorderTraverse(node.right);
  }
}
```

### sum BSTS

#### - JAVA Solution
```java
import java.util.*;

class Program {
    // This is an input class. Do not edit.
    static class BinaryTree {
        public int value;
        public BinaryTree left = null;
        public BinaryTree right = null;

        public BinaryTree(int value) {
            this.value = value;
        }
    }

    static class BTInfo{
        int size;
        int sum;
        int min;
        int max;
        boolean isBst;
        int total;

        public BTInfo(int size, int sum, int min, int max, boolean isBst, int total) {
            this.size = size;
            this.sum = sum;
            this.min = min;
            this.max = max;
            this.isBst = isBst;
            this.total = total;
        }
    }

    public int sumBsts(BinaryTree tree) {
        // Write your code here.
        BTInfo btInfo = sumBstsHelper(tree);
        return btInfo.total;
    }

    public BTInfo sumBstsHelper(BinaryTree node){
        if(node == null)
            return new BTInfo(0,0,Integer.MAX_VALUE,Integer.MIN_VALUE,true,0);

        BTInfo left = sumBstsHelper(node.left);
        BTInfo right = sumBstsHelper(node.right);
        int min = Math.min(Math.min(left.min, right.min), node.value);
        int max = Math.max(Math.max(left.max, right.max), node.value);
        boolean isBst = left.isBst && right.isBst && node.value> left.max && node.value<= right.min;
        int size = isBst ? left.size+right.size+1:0;
        int sum = isBst ? left.sum+right.sum+node.value:0;
        int totalSum = isBst&&size>=3 ? sum : left.total+ right.total;
        return new BTInfo(size,sum,min,max,isBst,totalSum);
    }
}

```

### right Smaller Than

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static List<Integer> rightSmallerThan(List<Integer> array) {
        // Write your code here.
        int n = array.size();
        List<Integer> ans = new ArrayList<>();
        for(int i=0;i<n;i++){
            int count = 0;
            for(int j=i+1;j<n;j++)
                if(array.get(i) > array.get(j))
                    count++;
            ans.add(count);
        }
        return ans;
    }
}

```
