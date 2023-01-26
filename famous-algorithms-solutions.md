## AlgoExpert Recursion Problems

### kadanes Algorithm

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

int kadanesAlgorithm(vector<int> a) {
  int sum =0,l=0,mx = INT_MIN,mn=INT_MIN;
  for(int i=0;i<a.size();i++){
    mn = max(mn,a[i]);
    if(sum+a[i] <= 0){
      l = i+1;
      sum = 0;
    }else{
      sum += a[i];
      if(sum>mx)
        mx = sum;
    }
  }
  return max(mn,mx);
}
```
### stable Internships

#### - CPP Solution
```cpp
using namespace std;
#include<stack>

vector<vector<int>> stableInternships(vector<vector<int>> interns, vector<vector<int>> teams) {
  stack<int> s;
  int n = teams.size();
  vector<unordered_map<int,int>> teamsMap;
  vector<int> lastInternsIndex(n,0);
  unordered_map<int,int> finalMatch;
  for(int i=0;i<n;i++)
    s.push(i);
  
  for(auto team:teams){
    unordered_map<int,int> m;
    for(int j=0;j<n;j++)
      m[team[j]] = j;
    teamsMap.push_back(m);
  }
  while(!s.empty()){
    int currentIntern = s.top();
    s.pop();
    int teamId = interns[currentIntern][lastInternsIndex[currentIntern]];
    lastInternsIndex[currentIntern]++;
    if(finalMatch.find(teamId) == finalMatch.end()){
        finalMatch[teamId] = currentIntern;
    }else{
      int prevIntern = finalMatch[teamId];
      int currentInternRank = teamsMap[teamId][currentIntern];
      int prevInternRank = teamsMap[teamId][prevIntern];
      if(currentInternRank < prevInternRank){
        finalMatch[teamId] = currentIntern;
        s.push(prevIntern);
      }else{
        s.push(currentIntern);
      }
    }
  }
  vector<vector<int>> ans;
  for (auto const& [key, val] : finalMatch)
  {
    ans.push_back({val,key});
  }
  return ans;
}
```
### Union Find

#### - CPP Solution
```cpp
#include <optional>
using namespace std;

// Do not edit the class below except for
// the constructor, push, pop, peek, and
// isEmpty methods. Feel free to add new
// properties and methods to the class.
class UnionFind {
  unordered_map<int,int> parents;
  unordered_map<int,int> ranks;
public:
  void createSet(int value) {
    // Write your code here.
    parents[value] = value;
    ranks[value] = 0;
  }

  optional<int> find(int value) {
    // Write your code here.
    if(parents.find(value) == parents.end())
      return nullopt;
    if(parents[value] != value)
      parents[value] = *find(parents[value]);
    return parents[value];
  }

  void createUnion(int valueOne, int valueTwo) {
    if(parents.find(valueOne) == parents.end() or parents.find(valueTwo) == parents.end())
      return;
    int valueOneRoot = *find(valueOne);
    int valueTwoRoot = *find(valueTwo);
    if(ranks[valueOneRoot]<ranks[valueTwoRoot])
      parents[valueOneRoot] = valueTwoRoot;
    else if(ranks[valueOneRoot]>ranks[valueTwoRoot])
      parents[valueTwoRoot] = valueOneRoot;
    else{
      parents[valueOneRoot] = valueTwoRoot;
      ranks[valueTwoRoot]++;
    }
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
