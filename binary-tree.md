## AlgoExpert Binary Tree Problems

### Branch Sums

#### - CPP Solution
```cpp
using namespace std;

// This is the class of the input root. Do not edit it.
class BinaryTree {
public:
  int value;
  BinaryTree *left;
  BinaryTree *right;

  BinaryTree(int value) {
    this->value = value;
    left = nullptr;
    right = nullptr;
  }
};

void branchSumsHelper(BinaryTree *node,vector<int> &res,int sum) {
  if(node == nullptr)
    return;
  if(node->left == nullptr && node->right == nullptr){
    res.push_back(sum+node->value);
    return;
  }
  branchSumsHelper(node->left,res,sum+node->value);
  branchSumsHelper(node->right,res,sum+node->value);
}

vector<int> branchSums(BinaryTree *root) {
  vector<int> res;
  branchSumsHelper(root,res,0);
  return res;
}
```
### Node Depths

#### - CPP Solution
```cpp
using namespace std;

class BinaryTree {
public:
  int value;
  BinaryTree *left;
  BinaryTree *right;

  BinaryTree(int value) {
    this->value = value;
    left = nullptr;
    right = nullptr;
  }
};
int nodeDepthsHelper(BinaryTree *root,int depth) {
  if(root == nullptr) 
    return 0;
  return depth + nodeDepthsHelper(root->left,depth+1) + nodeDepthsHelper(root->right,depth+1);
}
int nodeDepths(BinaryTree *root) {
  return nodeDepthsHelper(root,0);
}
```
### Evaluate Expression Tree

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

  public int evaluateExpressionTree(BinaryTree tree) {
    if(tree.left == null || tree.right == null)
      return tree.value;
    int left = evaluateExpressionTree(tree.left);
    int right = evaluateExpressionTree(tree.right);
    if(tree.value == -1)
      return left + right;
    if(tree.value == -2)
      return left - right;
    if(tree.value == -3)
      return left / right;
    return left * right;
  }
}
```
### Invert Binary Tree

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public static void invertBinaryTree(BinaryTree tree) {
    if(tree == null)
      return;
    BinaryTree temporary = tree.right;
    tree.right = tree.left;
    tree.left = temporary;
    invertBinaryTree(tree.left);
    invertBinaryTree(tree.right);
  }

  static class BinaryTree {
    public int value;
    public BinaryTree left;
    public BinaryTree right;

    public BinaryTree(int value) {
      this.value = value;
    }
  }
}
```
### Binary Tree Diameter

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

  public int binaryTreeDiameter(BinaryTree tree) {
    TreeInfo res = getTreeDiameter(tree);
    return res.diameter;
  }
  public TreeInfo getTreeDiameter(BinaryTree tree) {
    if(tree == null)
      return new TreeInfo(0,0);
    TreeInfo left = getTreeDiameter(tree.left);
    TreeInfo right = getTreeDiameter(tree.right);
    int diameter = Math.max(left.height+right.height,Math.max(left.diameter,right.diameter));
    int height = Math.max(left.height,right.height) + 1;
    return new TreeInfo(diameter,height);
  }
  static class TreeInfo{
    int diameter;
    int height;
    TreeInfo(int d,int h){
      diameter = d;
      height = h;
    }
  }
}
```
### Find Successor

#### - JAVA Solution
```java
import java.util.*;

class Program {
    // This is an input class. Do not edit.
    static class BinaryTree {
        public int value;
        public BinaryTree left = null;
        public BinaryTree right = null;
        public BinaryTree parent = null;

        public BinaryTree(int value) {
            this.value = value;
        }
    }

    public BinaryTree findSuccessor(BinaryTree tree, BinaryTree node) {
        if(tree == null)
            return null;
        BinaryTree left = findSuccessor(tree.left,node);
        if(tree == node){
            if(tree.right != null)
                return getNext(tree.right);
            if(tree.parent != null && tree.parent.left == tree)
                return tree.parent;
            if(tree.parent != null && tree.parent.right == tree)
                return tree.parent.parent;
        }
        BinaryTree right = findSuccessor(tree.right,node);
        return left == null ? right:left;
    }

    private BinaryTree getNext(BinaryTree right) {
        if(right == null)
            return null;
        if(right.left == null)
            return right;
        return getNext(right.left);
    }

}
```
### Height Balanced Binary Tree

#### - CPP Solution
```cpp
using namespace std;

// This is an input class. Do not edit.
class BinaryTree {
public:
  int value;
  BinaryTree *left = nullptr;
  BinaryTree *right = nullptr;

  BinaryTree(int value) { this->value = value; }
};
struct TreeInfo{
  bool isBalanced;
  int hight;
};
TreeInfo dfs(BinaryTree *node) {
  if(node == nullptr)
    return TreeInfo{true,-1};
  TreeInfo left = dfs(node->left);
  TreeInfo right = dfs(node->right);
  bool isBalanced = left.isBalanced and right.isBalanced and 
    abs(left.hight - right.hight) <= 1;
  return TreeInfo{isBalanced,max(left.hight , right.hight)+1};
}
bool heightBalancedBinaryTree(BinaryTree *tree) {
  TreeInfo treeInfo = dfs(tree);
  return treeInfo.isBalanced;
}
```

### Merge Binary Trees

#### - CPP Solution
```cpp
using namespace std;

// This is an input class. Do not edit.
class BinaryTree {
public:
  int value;
  BinaryTree *left = nullptr;
  BinaryTree *right = nullptr;

  BinaryTree(int value) {
    this->value = value;
  }
};
BinaryTree* mergeBinaryTrees(BinaryTree* t1, BinaryTree* t2) {
  if(t1 != nullptr and t2 != nullptr){
    t1->value = t1->value + t2->value;
    t1->left = mergeBinaryTrees(t1->left,t2->left);
    t1->right = mergeBinaryTrees(t1->right,t2->right);
  }else if(t1 != nullptr)
    t1 = t1;
  else if(t2 != nullptr)
    t1 = t2;
  else
    return nullptr;
  return t1;
}
```
### Symmetrical Tree

#### - CPP Solution
```cpp
using namespace std;

// This is an input class. Do not edit.
class BinaryTree {
public:
  int value;
  BinaryTree *left = nullptr;
  BinaryTree *right = nullptr;

  BinaryTree(int value) {
    this->value = value;
  }
};
bool symmetricalTreeHelper(BinaryTree* left,BinaryTree* right) {
  // Write your code here.
  if(!left and !right)
    return true;
  if(left and right and left->value == right->value)
    return symmetricalTreeHelper(left->left,right->right) and
    symmetricalTreeHelper(left->right,right->left);
  return false;
}

bool symmetricalTree(BinaryTree* tree) {
  if(!tree)
    return true;
  return symmetricalTreeHelper(tree->left,tree->right);
}
```
### Split Binary Tree

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
    
    public int calculateBTSum(BinaryTree tree){
        if(tree == null)
            return 0;
        int sum = 0;
        sum+=tree.value;
        sum += calculateBTSum(tree.left)+calculateBTSum(tree.right);
        return sum;
    }

    public TreeInfo checkBTEdgeSum(BinaryTree tree,int targetSum){
        if(tree == null)
            return new TreeInfo(0,false);
        TreeInfo left = checkBTEdgeSum(tree.left,targetSum);
        TreeInfo right = checkBTEdgeSum(tree.right,targetSum);
        int currentSum = tree.value + left.sum + right.sum;
        boolean canSplit = currentSum == targetSum || left.check || right.check;
        return new TreeInfo(currentSum,canSplit);
    }

    public int splitBinaryTree(BinaryTree tree) {
        // Write your code here.
        int sum = calculateBTSum(tree);
        if(sum == 0 || sum%2 != 0)
            return 0;
        TreeInfo treeInfo = checkBTEdgeSum(tree,sum/2);
        if(treeInfo.check)
            return sum/2;
        return 0;
    }

    private class TreeInfo {
        int sum = 0;
        boolean check = false;

        public TreeInfo(int sum, boolean check) {
            this.sum = sum;
            this.check = check;
        }
    }
}
```
### Max Path Sum In Binary Tree

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int maxSum;
    public static int maxPathSum(BinaryTree tree) {
        // Write your code here.
        maxSum = tree.value;
        maxPathSumHelper(tree);
        return maxSum;
    }

    private static int maxPathSumHelper(BinaryTree tree) {
        if(tree == null)
            return 0;
        int left = maxPathSumHelper(tree.left);
        int right = maxPathSumHelper(tree.right);
        maxSum = Math.max(maxSum,Math.max(left+right + tree.value,Math.max(right + tree.value,left + tree.value)));
        return Math.max(left,right) + tree.value;
    }

    static class BinaryTree {
        public int value;
        public BinaryTree left;
        public BinaryTree right;

        public BinaryTree(int value) {
            this.value = value;
        }
    }
}
```
### Find Nodes Distance K

#### - CPP Solution
```cpp
using namespace std;

// This is an input class. Do not edit.
class BinaryTree {
public:
  int value;
  BinaryTree *left = nullptr;
  BinaryTree *right = nullptr;

  BinaryTree(int value) { this->value = value; }
};
void convertBTToGraph(BinaryTree* tree,unordered_map<int,vector<int>>&graph){
  if(tree == nullptr)
    return;
  if(tree->left != nullptr){
    graph[tree->value].push_back(tree->left->value);
    graph[tree->left->value].push_back(tree->value);
    convertBTToGraph(tree->left,graph);
  }
  if(tree->right != nullptr){
    graph[tree->value].push_back(tree->right->value);
    graph[tree->right->value].push_back(tree->value);
    convertBTToGraph(tree->right,graph);
  }
}
vector<int> findNodesDistanceK(BinaryTree *tree, int target, int k) {
  // convert BT to graph
  unordered_map<int,vector<int>> graph;
  vector<int> ans;
  convertBTToGraph(tree,graph);
  queue<int>q;
  unordered_set<int> vis;
  q.push(target);
  while(!q.empty() and k > 0){
    int sz = q.size();
    while(sz--){
      int curr = q.front();
      q.pop();
      vis.insert(curr);
      for(int child : graph[curr])
        if(vis.find(child) == vis.end())
          q.push(child); 
    }
    k--;
  }
  while(!q.empty()){
    ans.push_back(q.front());
    q.pop();
  }
  return ans;
}
```
### Right Sibling Tree Helper

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

// This is the class of the input root. Do not edit it.
class BinaryTree {
public:
  int value;
  BinaryTree *left = nullptr;
  BinaryTree *right = nullptr;

  BinaryTree(int value);
};

void rightSiblingTreeHelper(BinaryTree *node,BinaryTree *parent,bool isLeft) {
  if(!node)
    return;
  BinaryTree *left = node->left,*right = node->right;
  rightSiblingTreeHelper(left,node,true);
  if(!parent)
    node->right = nullptr;
  else if(isLeft){
    node->right = parent->right;
  }else{
    if(!parent->right)
      node->right = nullptr;
    else
      node->right = parent->right->left;
  }
  rightSiblingTreeHelper(right,node,false);
}

BinaryTree *rightSiblingTree(BinaryTree *root) {
  rightSiblingTreeHelper(root,nullptr,false);
  return root;
}
```
### Iterative InOrder Traversal

#### - JAVA Solution
```java
import java.util.function.Function;

class Program {
    public static void iterativeInOrderTraversal(
            BinaryTree tree, Function<BinaryTree, Void> callback
    ) {
        // Write your code here.
        BinaryTree curr = tree;
        BinaryTree prev = null;
        while (curr != null){
            BinaryTree temp = curr;
            if(prev == null || prev == curr.parent){
                if(curr.left != null){
                    curr = curr.left;
                }else {
                    callback.apply(curr);
                    curr = curr.right == null ? curr.parent : curr.right;
                }

            }else if(prev == curr.left){
                callback.apply(curr);
                curr = curr.right == null ? curr.parent : curr.right;
            }else{
                curr = curr.parent;
            }
            prev = temp;
        }
    }

    static class BinaryTree {
        public int value;
        public BinaryTree left;
        public BinaryTree right;
        public BinaryTree parent;

        public BinaryTree(int value) {
            this.value = value;
        }

        public BinaryTree(int value, BinaryTree parent) {
            this.value = value;
            this.parent = parent;
        }
    }
}
```
### Flatten Binary Tree

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static BinaryTree flattenBinaryTree(BinaryTree root) {
        // Write your code here.
        List<BinaryTree> out = new ArrayList<>();
        inOrderTraverse(root,out);
        for(int i=0;i< out.size()-1;i++){
            out.get(i).right = out.get(i+1);
            out.get(i+1).left = out.get(i);
        }
        return out.get(0);
    }
    
    private static void inOrderTraverse(BinaryTree node,List<BinaryTree> out){
        if(node == null)
            return;
        inOrderTraverse(node.left,out);
        out.add(node);
        inOrderTraverse(node.right,out);
    }

    // This is the class of the input root. Do not edit it.
    static class BinaryTree {
        int value;
        BinaryTree left = null;
        BinaryTree right = null;

        public BinaryTree(int value) {
            this.value = value;
        }
    }
}
```

#### - Another Solution
```java

```
### Right Sibling Tree

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

// This is the class of the input root. Do not edit it.
class BinaryTree {
public:
  int value;
  BinaryTree *left = nullptr;
  BinaryTree *right = nullptr;

  BinaryTree(int value);
};

void rightSiblingTreeHelper(BinaryTree *node,BinaryTree *parent,bool isLeft) {
  if(!node)
    return;
  BinaryTree *left = node->left,*right = node->right;
  rightSiblingTreeHelper(left,node,true);
  if(!parent)
    node->right = nullptr;
  else if(isLeft){
    node->right = parent->right;
  }else{
    if(!parent->right)
      node->right = nullptr;
    else
      node->right = parent->right->left;
  }
  rightSiblingTreeHelper(right,node,false);
}

BinaryTree *rightSiblingTree(BinaryTree *root) {
  rightSiblingTreeHelper(root,nullptr,false);
  return root;
}
```
### All Kinds Of Node Depths

#### - JAVA Solution
```java
import java.util.*;

class Program {
    // average case : O(nlog(n)) time | O(h) space
    public static int allKindsOfNodeDepths(BinaryTree root) {
        // Write your code here.
        if(root == null)
            return 0;
        return nodeDepths(root,0) + allKindsOfNodeDepths(root.left) + allKindsOfNodeDepths(root.right);
    }

    static int nodeDepths(BinaryTree root,int depth) {
        if(root == null)
            return 0;
        return depth + nodeDepths(root.left,depth+1) + nodeDepths(root.right,depth+1);
    }

    static class BinaryTree {
        int value;
        BinaryTree left;
        BinaryTree right;

        public BinaryTree(int value) {
            this.value = value;
            left = null;
            right = null;
        }
    }
}
```

#### - Optimal Solution
```java
import java.util.*;

class Program {
    // O(n) time | O(n) space
    public static int allKindsOfNodeDepths(BinaryTree root) {
        // Write your code here.
        Map<BinaryTree,Integer> count = new HashMap<>();
        Map<BinaryTree,Integer> depth = new HashMap<>();
        nodeCount(root,count);
        nodeDepth(root,count,depth);
        return sumAllDepth(root,depth);
    }

    private static int sumAllDepth(BinaryTree root, Map<BinaryTree, Integer> depth) {
        if(root == null)
            return 0;
        return depth.get(root) + sumAllDepth(root.left,depth) + sumAllDepth(root.right,depth);
    }

    private static void nodeDepth(BinaryTree root, Map<BinaryTree, Integer> count, Map<BinaryTree, Integer> depth) {
        depth.put(root,0);
        if(root.left != null){
            nodeDepth(root.left,count,depth);
            int total = depth.get(root) + depth.get(root.left) + count.get(root.left);
            depth.put(root,total);
        }
        if(root.right != null){
            nodeDepth(root.right,count,depth);
            int total = depth.get(root) + depth.get(root.right) + count.get(root.right);
            depth.put(root,total);
        }
    }

    private static void nodeCount(BinaryTree root, Map<BinaryTree, Integer> count) {
        count.put(root,1);
        if(root.left != null){
            nodeCount(root.left,count);
            int total = count.get(root) + count.get(root.left);
            count.put(root,total);
        }
        if(root.right != null){
            nodeCount(root.right,count);
            int total = count.get(root) + count.get(root.right);
            count.put(root,total);
        }
    }


    static class BinaryTree {
        int value;
        BinaryTree left;
        BinaryTree right;

        public BinaryTree(int value) {
            this.value = value;
            left = null;
            right = null;
        }
    }
}
```

#### - Most optimal Solution

```java
import java.util.*;

class Program {
    // O(n) time | O(h) space
    public static int allKindsOfNodeDepths(BinaryTree root) {
        return getTreeInfo(root).allDepthSum;
    }

    public static TreeInfo getTreeInfo(BinaryTree root){
        if(root == null)
            return new TreeInfo(0,0,0);
        TreeInfo left = getTreeInfo(root.left);
        TreeInfo right = getTreeInfo(root.right);
        int numOfNode = 1 + left.totalNodes + right.totalNodes;
        int depth = left.depth + left.totalNodes + right.depth + right.totalNodes;
        int totalDepth = depth + left.allDepthSum + right.allDepthSum;
        return new TreeInfo(totalDepth,depth,numOfNode);
    }


    static class TreeInfo{
        int allDepthSum;
        int depth;
        int totalNodes;

        public TreeInfo(int allDepthSum, int depth, int totalNodes) {
            this.allDepthSum = allDepthSum;
            this.depth = depth;
            this.totalNodes = totalNodes;
        }
    }


    static class BinaryTree {
        int value;
        BinaryTree left;
        BinaryTree right;

        public BinaryTree(int value) {
            this.value = value;
            left = null;
            right = null;
        }
    }
}
```

### Compare Leaf Traversal

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
    // O(n+m) time | O(h1+h2) space
    public boolean compareLeafTraversal(BinaryTree tree1, BinaryTree tree2) {
        // Write your code here.
        Stack<BinaryTree> s1 = new Stack<>();
        s1.push(tree1);
        Stack<BinaryTree> s2 = new Stack<>();
        s2.push(tree2);
        while(!s1.empty() && !s2.empty()){
            BinaryTree leaf1 = getNextLeafNode(s1);
            BinaryTree leaf2 = getNextLeafNode(s2);
            if(leaf1.value != leaf2.value)
                return false;
        }
        return s1.empty() && s2.empty();
    }

    private BinaryTree getNextLeafNode(Stack<BinaryTree> stack) {
        while(true){
            BinaryTree node = stack.pop();
            if(node.left == null && node.right == null)
                return node;
            if(node.left != null)
                stack.push(node.left);
            if(node.right != null)
                stack.push(node.right);
        }
    }
}
```

#### - Another Optimal Solution
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
    // O(n+m) time | O(max(h1+h2)) space
    public boolean compareLeafTraversal(BinaryTree tree1, BinaryTree tree2) {
        // Write your code here.
        BinaryTree list1LeafNodesLinkedList = connectBTLeafNodes(tree1,null,null)[0];
        BinaryTree list2LeafNodesLinkedList = connectBTLeafNodes(tree2,null,null)[0];

        while(list1LeafNodesLinkedList != null && list2LeafNodesLinkedList != null){
            if(list1LeafNodesLinkedList.value != list2LeafNodesLinkedList.value)
                return false;
            list1LeafNodesLinkedList = list1LeafNodesLinkedList.right;
            list2LeafNodesLinkedList = list2LeafNodesLinkedList.right;
        }
        return list1LeafNodesLinkedList == null && list2LeafNodesLinkedList == null;
    }

    private BinaryTree[] connectBTLeafNodes(BinaryTree current,BinaryTree head,BinaryTree prev) {
        if(current == null)
            return new BinaryTree[]{head,prev};
        if(current.right == null && current.left == null){
            if(head == null){
                head = current;
            }else{
                prev.right = current;
            }
            prev = current;
        }
        BinaryTree[] left = connectBTLeafNodes(current.left,head,prev);
        return connectBTLeafNodes(current.right,left[0],left[1]);
    }

}
```
