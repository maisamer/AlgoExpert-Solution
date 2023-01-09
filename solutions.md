## AlgoExpert Recursion 

### Nth Fibonacci

#### - java Solution
```java
import java.util.*;

class Program {
  public static int getNthFib(int n) {
    if(n==1)
      return 0;
    int ans=1,f1=0,f2=1;
    for(int i=2;i<n;i++){
      ans = f1+f2;
      f1 = f2;
      f2 = ans;
    }
    return ans;
  }
}
```
### Permutations

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
void getPermutations(vector<int> array,vector<vector<int>>& ans,int i){
  if(i>=array.size()){
    ans.push_back(array);
    return;
  }
  for(int j=i;j<array.size();j++){
    swap(array[i],array[j]);
    getPermutations(array,ans,i+1);
    swap(array[i],array[j]);   
  } 
}
vector<vector<int>> getPermutations(vector<int> array) {
  if(array.size() == 0)
      return {};
  vector<vector<int>> ans;
  getPermutations(array,ans,0);
  return ans;
}
```
### Powerset

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
void powerset(vector<vector<int>>& ans ,vector<int> array,vector<int> subAns,int i) {
  if(i >= array.size()){
    ans.push_back(subAns);
    return;
  }
  powerset(ans,array,subAns,i+1);
  subAns.push_back(array[i]);
  powerset(ans,array,subAns,i+1);
}
vector<vector<int>> powerset(vector<int> array) {
  vector<vector<int>> ans ;
  powerset(ans,array,{},0);
  return ans;
}
```
