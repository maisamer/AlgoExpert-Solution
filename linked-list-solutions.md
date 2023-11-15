## AlgoExpert Linked List Problems

### Remove duplicated from linked list

#### - CPP Solution
```cpp
using namespace std;

// This is an input struct. Do not edit.
class LinkedList {
public:
  int value;
  LinkedList *next = nullptr;

  LinkedList(int value) { this->value = value; }
};

LinkedList *removeDuplicatesFromLinkedList(LinkedList *list) {
  LinkedList *curr = list;
  while(curr != nullptr and curr->next != nullptr){
    if(curr->value == curr->next->value){
      curr->next = curr->next->next;
      continue;
    }
    curr = curr->next;
  }
  return list;
}
```

### Middle Node

#### - JAVA Solution
```java
import java.util.*;

class Program {
  // This is an input class. Do not edit.
  public static class LinkedList {
    public int value;
    public LinkedList next;

    public LinkedList(int value) {
      this.value = value;
      this.next = null;
    }
  }

  public LinkedList middleNode(LinkedList linkedList) {
    // Write your code here.
    int len = 0;
    LinkedList curr = linkedList;
    while(curr != null){
      len++;
      curr = curr.next;
    }
    int mid = len/2;
    LinkedList midNode = linkedList;
    while(mid > 0){
      midNode = midNode.next;
      mid--;
    }
    return midNode;
  }
}
```

#### - another Solution
```java
import java.util.*;

class Program {
  // This is an input class. Do not edit.
  public static class LinkedList {
    public int value;
    public LinkedList next;

    public LinkedList(int value) {
      this.value = value;
      this.next = null;
    }
  }

  public LinkedList middleNode(LinkedList linkedList) {
    // Write your code here.
    LinkedList slow = linkedList;
    LinkedList fast = linkedList;
    while(fast != null && fast.next != null){
      slow = slow.next;
      fast = fast.next.next;
    }
    return slow;
  }
}
```

### Linked List Construction

#### - JAVA Solution
```java
import java.util.*;

// Feel free to add new properties and methods to the class.
class Program {
    static class DoublyLinkedList {
        public Node head;
        public Node tail;

        public void setHead(Node node) {
            // Write your code here.
            if(head == null) {
                tail = node;
                head = node;
              return;
            }
          insertBefore(head,node);
        }

        public void setTail(Node node) {
            // Write your code here.
            if(tail == null){
                setHead(node);
              return;
            }
          insertAfter(tail,node);
        }

        public void insertBefore(Node node, Node nodeToInsert) {
            if(nodeToInsert == head && nodeToInsert == tail) return;
            remove(nodeToInsert);
            nodeToInsert.next = node;
            nodeToInsert.prev = node.prev;
            if(node.prev == null)
              head = nodeToInsert;
            else 
              node.prev.next = nodeToInsert;
            node.prev = nodeToInsert;     
        }

        public void insertAfter(Node node, Node nodeToInsert) {
            if(nodeToInsert == head && nodeToInsert == tail) return;
            remove(nodeToInsert);
            nodeToInsert.next = node.next;
            nodeToInsert.prev = node;
            if(node.next == null)
              tail = nodeToInsert;
            else
              node.next.prev = nodeToInsert;
            node.next = nodeToInsert;
        }

        public void insertAtPosition(int position, Node nodeToInsert) {
            // Write your code here.
            if(position == 1){
                setHead(nodeToInsert);
                return;
            }
            int counter = 1;
            Node curr = head;
            while (curr != null && counter<position){
                counter++;
                curr = curr.next;
            }
            if(curr != null)
             insertBefore(curr,nodeToInsert);
            else
              setTail(nodeToInsert);
        }

        public void removeNodesWithValue(int value) {
            // Write your code here.
            Node curr = head;
            while (curr != null){
                Node nodeToRemove = curr;
                curr=curr.next;
                if (nodeToRemove.value == value)
                    remove(nodeToRemove);       
            }
        }

        public void remove(Node node) {
            if(node == head) head = head.next;
            if(node == tail) tail = tail.prev;
            if(node.prev != null) node.prev.next = node.next;
            if(node.next != null) node.next.prev = node.prev;
            node.prev = null;
            node.next = null;
        }

        public boolean containsNodeWithValue(int value) {
            // Write your code here.
            Node curr = head;
            while(curr != null){
                if(curr.value == value)
                    return true;
                curr = curr.next;
            }
            return false;
        }
    }

    // Do not edit the class below.
    static class Node {
        public int value;
        public Node prev;
        public Node next;

        public Node(int value) {
            this.value = value;
        }
    }
}
```

### Sum Of Linked Lists

#### - JAVA Solution
```java
import java.util.*;

class Program {
    // This is an input class. Do not edit.
    public static class LinkedList {
        public int value;
        public LinkedList next;

        public LinkedList(int value) {
            this.value = value;
            this.next = null;
        }
    }

    public LinkedList sumOfLinkedLists(
            LinkedList linkedListOne, LinkedList linkedListTwo
    ) {
        // Write your code here.
        LinkedList dummy = new LinkedList(-1);
        LinkedList root = dummy;
        int carry = 0;
        while (linkedListOne != null || linkedListTwo != null || carry != 0){
            int sum = carry;
            if(linkedListOne != null) {
                sum += linkedListOne.value;
                linkedListOne = linkedListOne.next;
            }
            if(linkedListTwo != null) {
                sum += linkedListTwo.value;
                linkedListTwo = linkedListTwo.next;
            }
            root.next = new LinkedList(sum%10);
            carry = sum/10;
            root = root.next;
        }
        return dummy.next;
    }
}
```

### Remove Kth Node From End

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static void removeKthNodeFromEnd(LinkedList head, int k) {
        // Write your code here.
        if(head != null) {
            int length = head.length();
            int nodeInd = length-k;
            if(nodeInd == 0){
                head.value = head.next.value;
                head.next = head.next.next;
                return;
            }
            LinkedList curr = head;
            while(nodeInd>0){
                nodeInd--;
                if(nodeInd == 0){
                    curr.next = curr.next.next;
                }
                curr = curr.next;
            }
        }

    }

    static class LinkedList {
        int value;
        LinkedList next = null;

        public LinkedList(int value) {
            this.value = value;
        }
        public int length(){
            LinkedList curr = this;
            int length = 0;
            while (curr != null){
                curr = curr.next;
                length++;
            }
            return length;
        }
    }
}
```

### Merging Linked Lists

#### - JAVA Solution
```java
import java.util.*;

class Program {
    // This is an input class. Do not edit.
    public static class LinkedList {
        public int value;
        public LinkedList next;

        public LinkedList(int value) {
            this.value = value;
            this.next = null;
        }
        
        public int getLength(){
            LinkedList curr = this;
            int length = 0;
            while (curr != null){
                curr = curr.next;
                length++;
            }
            return length;
        }
    }

    public LinkedList mergingLinkedLists(
            LinkedList linkedListOne, LinkedList linkedListTwo
    ) {
        int l1 = linkedListOne.getLength(),l2 = linkedListTwo.getLength();
        while (Math.abs(l1-l2) != 0){
            if(l1 > l2){
                l1--;
                linkedListOne = linkedListOne.next;
            }else{
                l2--;
                linkedListTwo = linkedListTwo.next;
            }
        }
        while (linkedListTwo != null && linkedListTwo != null){
            if(linkedListOne.value == linkedListTwo.value)
                return linkedListOne;
            linkedListTwo = linkedListTwo.next;
            linkedListOne = linkedListOne.next;
        }
        return null;
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
### LRU Cashe

#### - JAVA Solution
```java
import java.util.*;

// Do not edit the class below except for the insertKeyValuePair,
// getValueFromKey, and getMostRecentKey methods. Feel free
// to add new properties and methods to the class.
class Program {
    static class LRUCache {
        int maxSize;
        int currSize;
        Map<String,Node> cache;
        DoublyLinkedList doublyLinkedList ;


        public LRUCache(int maxSize) {
            this.maxSize = maxSize > 1 ? maxSize : 1;
            this.cache = new HashMap<>();
            this.doublyLinkedList = new DoublyLinkedList();
            this.currSize = 0;
        }

        public void insertKeyValuePair(String key, int value) {
            // Write your code here.
            if(cache.containsKey(key)){
                cache.get(key).value = value;
            }else{
                if(currSize == maxSize)
                    evictLeastRecentNode();
                else
                    currSize++;
                cache.put(key,new Node(key,value));
            }
            updateMostRecent(cache.get(key));
            
        }

        private void updateMostRecent(Node node) {
            doublyLinkedList.setHead(node);
        }

        private void evictLeastRecentNode() {
            cache.remove(doublyLinkedList.tail.key);
            doublyLinkedList.removeTail();
        }

        public LRUResult getValueFromKey(String key) {
            // Write your code here.
            if(!cache.containsKey(key))
                return new LRUResult(false,-1);
            updateMostRecent(cache.get(key));
            return new LRUResult(true,cache.get(key).value);
            
        }

        public String getMostRecentKey() {
            // Write your code here.
            if(doublyLinkedList.head != null)
                return doublyLinkedList.head.key;
            return "";
        }
    }

    static class LRUResult {
        boolean found;
        int value;

        public LRUResult(boolean found, int value) {
            this.found = found;
            this.value = value;
        }
    }
    static class Node {
        public String key;
        public int value;
        public Node prev;
        public Node next;

        public Node(String key,int value) {
            this.value = value;
            this.key = key;
        }
        public void removeBindings() {
            if(prev != null) prev.next = next;
            if(next != null) next.prev = prev;
            prev = null;
            next = null;
        }
    }
    static class DoublyLinkedList {
        public Node head;
        public Node tail;

        public void setHead(Node node) {
            // Write your code here.
            if(head == node)
                return;
            else if(head == null) {
                tail = node;
                head = node;
            } else if(head == tail){
                tail.prev = node;
                head = node;
                head.next = tail;
            }else{
                if(tail == node)
                    removeTail();
                node.removeBindings();
                head.prev = node;
                node.next = head;
                head = node;
            }
        }


        public void removeTail() {
            // Write your code here.
            if(tail == null){
                return;
            }
            if(head == tail) {
                head = null;
                tail = null;
                return;
            }
            tail = tail.prev;
            tail.next = null;
        }

    }
}
```
