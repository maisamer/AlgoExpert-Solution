## AlgoExpert Array Problems

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
