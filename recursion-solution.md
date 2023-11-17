## AlgoExpert Recursion Problems

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
### Product Sum

#### - JAVA Solution
```java
import java.util.*;

class Program {
  // Tip: You can use `element instanceof ArrayList` to check whether an item
  // is an array or an integer.
  public static Integer productSum(List<Object> array,Integer depth){
    int ans = 0;
    for(int i=0;i<array.size();i++){
      if(array.get(i) instanceof ArrayList)
        ans = ans + productSum((List)array.get(i),depth+1);
      else
        ans = ans + (Integer) array.get(i);
    }
    return ans*depth;
  }
  public static int productSum(List<Object> array) {
    return productSum(array,1);
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

### Blackjack Probability

#### - JAVA Solution
```java
import java.util.*;

class Program {

    public float blackjackProbability(int target, int startingHand) {
        // Write your code here.
        Map<Integer,Float> memo = new HashMap<>();
        return Math.round(blackjackProbabilityHelper(target,startingHand,memo)*1000f)/1000f;
    }
    float blackjackProbabilityHelper(int target, int start, Map<Integer, Float> memo){
        if(start > target)
            return 1;
        if(start+4 >= target)
            return 0;
        if(memo.containsKey(start))
            return memo.get(start);
        float ans = 0;
        for(int i=1;i<=10;i++)
            ans += .1*blackjackProbabilityHelper(target,start+i, memo);

        memo.put(start,ans);
        return ans;
    }
}

```
### Reveal Minesweeper

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public String[][] revealMinesweeper(String[][] board, int row, int column) {
        int height = board.length, width = board[0].length;
        if(board[row][column].equals("M")){
            board[row][column] = "X";
            return board;
        }
        List<int[]> neighbors = getNeighbors(height,width,row,column);
        int minesCount = 0;
        for(int []neighbor:neighbors)
            if(board[neighbor[0]][neighbor[1]].equals("M"))
                minesCount++;
        board[row][column] = Integer.toString(minesCount);
        if(minesCount == 0)
            for(int []neighbor:neighbors)
                if(board[neighbor[0]][neighbor[1]].equals("H"))
                    revealMinesweeper(board,neighbor[0],neighbor[1]);
        return board;
    }

    private List<int[]> getNeighbors(int height,int width, int row, int column) {
        List<int[]> neighbors = new ArrayList<>();
        int [][] directions = new int[][]{new int[]{1,1},new int[]{-1,-1},new int[]{0,1},new int[]{0,-1},
                new int[]{-1,0},new int[]{1,0},new int[]{1,-1},new int[]{-1,1}};
        for(int i=0;i<8;i++){
            if(row+directions[i][0] >=0 && row+directions[i][0]<height
                    && column+directions[i][1] >=0 && column+directions[i][1]<width)
                neighbors.add(new int[]{row+directions[i][0],column+directions[i][1]});
        }
        return neighbors;
    }
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
### Interweaving Strings

#### - CPP Solution
```cpp
using namespace std;
bool rec(string one, string two, string three,int i,int j,int k) {
  if(i>= three.size() && j>=one.size() && k>=two.size())
    return true;
  bool vaild = (j < one.size() && k < two.size());
  if(vaild && three[i] == one[j] && three[i] == two[k]){
    return rec(one,two,three,i+1,j+1,k) || rec(one,two,three,i+1,j,k+1);
  }
  if(j < one.size() && three[i] == one[j])
    return rec(one,two,three,i+1,j+1,k);
  if(k < two.size() && three[i] == two[k])
    return rec(one,two,three,i+1,j,k+1);
  return false;
}
bool interweavingStrings(string one, string two, string three) {
  if(one.size() + two.size() != three.size())
    return false;
  return rec(one,two,three,0,0,0);
}
```
### Solve Sudoku

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
bool valid(vector<vector<int>> &board,int i,int j,int sol){
  for(int k=0;k<9;k++){
     if(board[i][k] == sol || board[k][j] == sol)
       return false;
  }
  i = (i/3) *3;
  j = (j/3) *3;
  for(int l=i;l<i+3;l++){
    for(int m=j;m<j+3;m++){
      if(board[l][m] == sol)
        return false;
    }
  }
  return true;
}
bool solveSudoku(vector<vector<int>> &board,int i,int j) {
  if(j == 9){
    j = 0;
    i++;
  }
  if(i == 9)
    return true;
  if(board[i][j] != 0)
    return solveSudoku(board,i,j+1);
  
  for(int sol = 1;sol < 10;sol++){
    if(valid(board,i,j,sol)){
      board[i][j] = sol;
      if(solveSudoku(board,i,j+1))
        return true;
      board[i][j] = 0;
    }
  }
  return false;
}
vector<vector<int>> solveSudoku(vector<vector<int>> board) {
  solveSudoku(board,0,0);
  return board;
}
```
### Generate Div Tags

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
void generateDivTags(vector<string> &ans,int op,int cl,string str) {
  if(!op && !cl){
    ans.push_back(str);
    return;
  }
  if(op)
    generateDivTags(ans,op-1,cl+1,str+"<div>");
  if(cl)
    generateDivTags(ans,op,cl-1,str+"</div>");
}

vector<string> generateDivTags(int numberOfTags) {
  vector<string> ans;
  generateDivTags(ans,numberOfTags,0,"");
  return ans;
}
```
### Ambiguous Measurements

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
map<string,int> m;
string getStr(int low,int high){
  return to_string(low)+":"+to_string(high);
}
bool canMeasure(vector<vector<int>> measuringCups, int low,
                           int high) {
  string key = getStr(low,high);
  if(m.find(key) != m.end())
    return m[key];
  
  if(low<=0 and high<=0)
    return false;
  
  bool ans = false;
  for(int i=0;i<measuringCups.size();i++){
      if(low<=measuringCups[i][0] and measuringCups[i][1] <=high)
        return true;
      int newLow = max(0,low-measuringCups[i][0]);
      int newHigh = max(0,high-measuringCups[i][1]);
      ans = canMeasure(measuringCups,newLow,newHigh);
      if(ans)
         return true;
  }
  m[key] = ans;
  return ans;
}
bool ambiguousMeasurements(vector<vector<int>> measuringCups, int low,
                           int high) {
  m = {};
  return canMeasure(measuringCups,low,high);
}
```
### Number of binary tree topologies

#### - CPP Solution
```cpp
using namespace std;
map<int,int>m;
int rec(int n) {
  if(n == 0)
    return 1;
  if(m[n])
    return m[n];
  int ans = 0;
  for(int i=0;i<n;i++){
    ans += rec(i)*rec(n-1-i);
  }
  m[n] = ans;
  return ans;
}
int numberOfBinaryTreeTopologies(int n) {
  m = {};
  if(n <= 1)
    return 1;
  return rec(n);
}
```
### Non-attacking queens

#### - CPP Solution
```cpp
using namespace std;
bool valid(vector<vector<char>> grid,int n,int r,int c){
    for(int t=0;t<n;t++)
        if(grid[r][t] == 'q' or grid[t][c] == 'q')
            return false;
    for(int i=r,j=c;i<n&&j<n;i++,j++)
        if(grid[i][j] == 'q')
            return false;
    for(int i=r,j=c;i>=0&&j>=0;i--,j--)
        if(grid[i][j] == 'q')
            return false;
    for(int i=r,j=c;i>=0&&j<n;i--,j++)
        if(grid[i][j] == 'q')
            return false;
    for(int i=r,j=c;i<0&&j>=n;i++,j--)
        if(grid[i][j] == 'q')
            return false;
    return true;
}
int nonAttackingQueens(int r,int n,vector<vector<char>>grid) {
  if(r == n)
    return 1;
  int count = 0;
  for(int c=0;c<n;c++){
    if(grid[r][c] == '.' and valid(grid,n,r,c)){
      grid[r][c] = 'q';
      count+=nonAttackingQueens(r+1,n,grid);
      grid[r][c] = '.';
    }
  }
  return count;
}
int nonAttackingQueens(int n) {
  vector<vector<char>>grid (n,vector<char>(n,'.'));
  return nonAttackingQueens(0,n,grid);
}
```
### 

#### - CPP Solution
```cpp
```
