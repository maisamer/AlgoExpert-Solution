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
