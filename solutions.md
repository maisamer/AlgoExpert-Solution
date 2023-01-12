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
### Phone number mnemonics

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
map<char,string> m;
void recursion(string phoneNumber,vector<string>& ans,string opt,int i){
  if(i >= phoneNumber.size()){
    ans.push_back(opt);
    return;
  }
  for(int j=0;j<m[phoneNumber[i]].size();j++){
    recursion(phoneNumber,ans,opt+m[phoneNumber[i]][j], i+1);
  }
}
vector<string> phoneNumberMnemonics(string phoneNumber) {
  m['0'] = "0";
  m['1'] = "1";
  m['2'] = "abc";
  m['3'] = "def";
  m['4'] = "ghi";
  m['5'] = "jkl";
  m['6'] = "mno";
  m['7'] = "pqrs";
  m['8'] = "tuv";
  m['9'] = "wxyz";
  vector<string> ans;
  recursion(phoneNumber,ans,"", 0);
  return ans;
}
```
### Staircase traversal

#### - CPP Solution
```cpp
using namespace std;

int rec(int height, int maxSteps) {
  if(height == 0){
    return 1;
  }
  int ans = 0;
  for(int i=1;i<=maxSteps && height-i>= 0;i++){
    ans += rec(height-i,maxSteps);
  }
  return ans;
}
int staircaseTraversal(int height, int maxSteps) {
  if(height == 0) return 0;
  return rec(height,maxSteps);
}
```
### Lowest Common Manager

#### - CPP Solution
```cpp
using namespace std;
class OrgChart {
public:
  char name;
  vector<OrgChart *> directReports;

  OrgChart(char name) {
    this->name = name;
    this->directReports = {};
  }

  void addDirectReports(vector<OrgChart *> directReports);
};
int getLowestCommonManager(OrgChart *topManager, OrgChart *reportOne,
                                 OrgChart *reportTwo,OrgChart *&res) {
  int counter = 0;
  if(topManager->name == reportOne->name || topManager->name == reportTwo->name)
    counter++;
  for(auto &child:topManager->directReports)
    counter += getLowestCommonManager(child,reportOne,reportTwo,res);
  if(counter == 2){
    res = topManager;
    return 0;
  }
  return counter;
}
OrgChart *getLowestCommonManager(OrgChart *topManager, OrgChart *reportOne,
                                 OrgChart *reportTwo) {
  OrgChart *&res = topManager;
  getLowestCommonManager(topManager,reportOne,reportTwo,res);
  return res;
}
```
