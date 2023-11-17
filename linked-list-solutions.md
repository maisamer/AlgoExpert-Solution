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

### Find Loop

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public static LinkedList findLoop(LinkedList head) {
    // Write your code here.
    LinkedList slow=head,fast=head;
    while(fast!= null && fast.next != null){
      slow = slow.next;
      fast = fast.next.next;
      if(slow == fast)
        break;
    }
    slow = head;
    while(fast!= slow){
      slow = slow.next;
      fast = fast.next;
    }
    return slow;
  }

  static class LinkedList {
    int value;
    LinkedList next = null;

    public LinkedList(int value) {
      this.value = value;
    }
  }
}
```

### Reverse Linked List

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public static LinkedList reverseLinkedList(LinkedList head) {
    // Write your code here.
    LinkedList prev = null;
    LinkedList curr = head;
    while(curr != null){
      LinkedList temp = curr.next;
      curr.next = prev;
      prev = curr;
      curr = temp;
    }
    return prev;
  }

  static class LinkedList {
    int value;
    LinkedList next = null;

    public LinkedList(int value) {
      this.value = value;
    }
  }
}
```

### Merge Linked Lists

#### - JAVA Solution
```java
import java.util.*;

class Program {
  // This is an input class. Do not edit.
  public static class LinkedList {
    int value;
    LinkedList next;

    LinkedList(int value) {
      this.value = value;
      this.next = null;
    }
  }

  public static LinkedList mergeLinkedLists(
    LinkedList headOne, LinkedList headTwo
  ) {
    // Write your code here.
    LinkedList dummy = new LinkedList(-1);
    LinkedList curr = dummy;
    while(headOne != null || headTwo != null){
      if(headOne == null){
        curr.next = headTwo;
        headTwo = headTwo.next;
      }else if(headTwo == null){
        curr.next = headOne;
        headOne = headOne.next;
      }else{
        if(headOne.value < headTwo.value){
          curr.next = headOne;
          headOne = headOne.next;
        }else{
          curr.next = headTwo;
          headTwo = headTwo.next;
        }
      }
      curr = curr.next;
    }
    return dummy.next;
  }
}
```

### Another Solution

#### - JAVA Solution
```java
import java.util.*;

class Program {
  // This is an input class. Do not edit.
  public static class LinkedList {
    int value;
    LinkedList next;

    LinkedList(int value) {
      this.value = value;
      this.next = null;
    }
  }

  public static LinkedList mergeLinkedLists(
    LinkedList headOne, LinkedList headTwo
  ) {
    // Write your code here.
    LinkedList p1 = headOne , p2 = headTwo,prev=null;
    while(p1 != null && p2 != null){
      if(p1.value<p2.value){
        prev = p1;
        p1 = p1.next;
      }else{
        if(prev != null) prev.next = p2;
        prev = p2;
        p2 = p2.next;
        prev.next = p1;
      }
    }
    if(p1 == null)
      prev.next = p2;
    
    return headOne.value < headTwo.value ? headOne:headTwo;
  }
}
```

### Shift Linked List

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static LinkedList shiftLinkedList(LinkedList head, int k) {
        int n = head.getLength();
        System.out.println(n);
        k%=n;
        if(k == 0)
            return head;
        LinkedList left = head,right = head,prev = head,curr = head,tail = null;
        if(k > 0){
            int idx = n - k + 1;
            while(idx > 1){
                prev = curr;
                left = curr.next;
                curr = curr.next;
                idx--;
            }
            while(curr != null){
                right = curr;
                curr = curr.next;
            }
            prev.next = null;
            right.next = head;
        }else{
            int idx = k*-1 ;
            while(idx > 0){
                right = curr;
                curr = curr.next;
                idx--;
            }
            while(curr != null){
                tail = curr;
                curr = curr.next;
            }
            LinkedList re = right.next ;
            right.next = null;
            tail.next = left;
            return re;
        }
        return left;

    }

    static class LinkedList {
        public int value;
        public LinkedList next;

        public LinkedList(int value) {
            this.value = value;
            next = null;
        }

        int getLength(){
            LinkedList curr = this;
            int len = 0;
            while(curr != null){
                len++;
                curr = curr.next;
            }
            return len;
        }
    }
}
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
### Rearrange Linked List

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static LinkedList rearrangeLinkedList(LinkedList head, int k) {
        // Write your code here.
        LinkedList smallHead = null,smallTail = null;
        LinkedList equalHead = null,equalTail = null;
        LinkedList bigHead = null,bigTail = null;
        LinkedList curr = head;
        while(curr != null){
            if(curr.value < k){
                LinkedList[] changes = growChangeLinkedList(smallHead,smallTail,curr);
                smallHead = changes[0];
                smallTail = changes[1];
            }
            else if(curr.value > k){
                LinkedList[] changes = growChangeLinkedList(bigHead,bigTail,curr);
                bigHead = changes[0];
                bigTail = changes[1];
            }
            else {
                LinkedList[] changes = growChangeLinkedList(equalHead,equalTail,curr);
                equalHead = changes[0];
                equalTail = changes[1];
            }
            LinkedList prev = curr;
            curr = curr.next;
            prev.next = null;
        }
        LinkedList[] firstConnection = connectLinkedList(smallHead,smallTail,equalHead,equalTail);
        LinkedList[] finalConnection = connectLinkedList(firstConnection[0],firstConnection[1],bigHead,bigTail);
        return finalConnection[0];
    }

    private static LinkedList[] connectLinkedList(LinkedList headOne, LinkedList tailOne, LinkedList headTwo, LinkedList tailTwo) {
        LinkedList newHead = headOne == null ? headTwo:headOne;
        LinkedList newTail = tailTwo == null ? tailOne: tailTwo;
        if(tailOne != null)
            tailOne.next = headTwo;
        return new LinkedList[]{newHead,newTail};
    }

    private static LinkedList[] growChangeLinkedList(LinkedList head, LinkedList tail, LinkedList curr) {
        LinkedList[] changes = new LinkedList[]{head,curr};
        if(head == null)
            changes[0] = curr;
        if(tail != null)
            tail.next = curr;
        return changes;
    }

    static class LinkedList {
        public int value;
        public LinkedList next;

        public LinkedList(int value) {
            this.value = value;
            next = null;
        }
    }
}
```

### Linked List Palindrome

#### - JAVA Solution
```java
import java.util.*;

class Program {
    // This is an input class. Do not edit.

    public boolean linkedListPalindrome(LinkedList head) {
        // Write your code here.
        LinkedList slow = head,fast = head;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        LinkedList secondHalf = reversedSecondHalf(slow);
        LinkedList firstHalf = head;
        while (firstHalf != null && secondHalf != null){
            if(firstHalf.value != secondHalf.value)
                return false;
            firstHalf = firstHalf.next;
            secondHalf = secondHalf.next;
        }
        return true;
    }

    private LinkedList reversedSecondHalf(LinkedList head) {
        LinkedList curr = head;
        LinkedList prev = null;
        while(curr != null){
            LinkedList next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }

    public static class LinkedList {
        public int value;
        public LinkedList next = null;

        public LinkedList(int value) {
            this.value = value;
        }
    }
}
```

### Zip Linked List

#### - JAVA Solution
```java
import java.util.*;

class Program {
    // This is an input class. Do not edit.
    public LinkedList getMiddleNode(LinkedList head){
        LinkedList slow = head,fast = head;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        LinkedList secondHalf = slow.next;
        slow.next = null;
        return secondHalf;
    }
    private LinkedList reversedSecondHalf(LinkedList head) {
        LinkedList curr = head;
        LinkedList prev = null;
        while(curr != null){
            LinkedList next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }

    public LinkedList zipLinkedList(LinkedList linkedList) {
        // Write your code here.
        if(linkedList.next == null || linkedList.next.next == null)
            return linkedList;
        LinkedList firstHalf = linkedList;
        LinkedList secondHalf = getMiddleNode(linkedList);
        LinkedList reversedSecondHalf = reversedSecondHalf(secondHalf);

        return interweaveLinkedLists(firstHalf,reversedSecondHalf);
    }

    private LinkedList interweaveLinkedLists(LinkedList firstHalf, LinkedList secondHalf) {
        LinkedList firstIt = firstHalf,secondIt = secondHalf;
        while (firstIt != null && secondIt != null){
            LinkedList firstHalfNext = firstIt.next;
            LinkedList secondHalfNext = secondIt.next;
            firstIt.next = secondIt;
            secondIt.next = firstHalfNext;
            firstIt = firstHalfNext;
            secondIt = secondHalfNext;
        }
        return firstHalf;
    }


    public static class LinkedList {
        public int value;
        public LinkedList next;

        public LinkedList(int value) {
            this.value = value;
            this.next = null;
        }
    }
}
```

### Node Swap

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

    public LinkedList nodeSwap(LinkedList head) {
        // Write your code here.
        LinkedList curr = head;
        while (curr != null && curr.next!= null){
            int temp = curr.value;
            curr.value = curr.next.value;
            curr.next.value = temp;
            curr = curr.next.next;
        }
        return head;
    }
}
```
