## AlgoExpert Array Problems

### Two Number Sum

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

vector<int> twoNumberSum(vector<int> array, int targetSum) {
  sort(array.begin(),array.end());
  int l = 0, r = array.size() - 1;
  while(l < r){
    if(array[l]+array[r] == targetSum)
      return {array[l],array[r]};
    else if(array[l]+array[r] > targetSum)
      r--;
    else
      l++;
  }
  return {};
}
```
### Valid Subsequence

#### - CPP Solution
```cpp
using namespace std;

bool isValidSubsequence(vector<int> array, vector<int> sequence) {
  int l = 0;
  for(int i=0;i<array.size() and l<sequence.size();i++)
    if(array[i] == sequence[l])
      l++;
  return l == sequence.size();
}
```

### Sorted Squared Array

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

vector<int> sortedSquaredArray(vector<int> array) {
  vector<int> res(array.size(),0);
  int l = 0, r = array.size()-1,i = array.size()-1;
  while(l<=r){
    if(abs(array[l]) > abs(array[r])){
      res[i] = array[l]*array[l];
      l++;
    }else if(abs(array[l])<=abs(array[r])){
      res[i] = array[r]*array[r];
      r--;
    }
    i--;
  }
  return res;
}
```
### Tournament Winner

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

string tournamentWinner(vector<vector<string>> competitions,
                        vector<int> results) {
  unordered_map<string,int> dic;
  int mxResult = 0;
  string winningTeam;
  for(int i=0;i<results.size();i++){
    string team = results[i] == 0?competitions[i][1]:competitions[i][0];
    dic[team]++;
    if(dic[team]>mxResult){
      mxResult = dic[team];
      winningTeam = team;
    }
  }
  return winningTeam;
}
```
### nonConstructible Change

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

int nonConstructibleChange(vector<int> coins) {
  int change = 0;
  sort(coins.begin(),coins.end());
  for(int i=0;i<coins.size();i++){
    if(coins[i]>change+1)
      break;
    change+=coins[i];
  }
  return change+1;
}
```
### Transpose Matrix

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public int[][] transposeMatrix(int[][] matrix) {
    int r = matrix.length,c = matrix[0].length;
    int res[][] = new int[c][r];
    for(int i=0;i<c;i++){
      for(int j=0;j<r;j++){
        res[i][j] = matrix[j][i];
      }
    }   
    return res;
  }
}

```
### Three Number Sum

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

vector<vector<int>> threeNumberSum(vector<int> a, int targetSum) {
  vector<vector<int>>res;
  unordered_set<int> s;
  for(int i=0;i<a.size()-2;i++){
    unordered_set<int> s;
    for(int j=i+1;j<a.size();j++){
      int rem = targetSum-a[i]-a[j];
      if(s.find(rem) != s.end()){
        vector<int> subRes = {a[i],a[j],rem};
        sort(subRes.begin(),subRes.end());
        res.push_back(subRes); 
      }
      
      s.insert(a[j]);
    }
  }
  return res;
}
```

#### - Another Solution
```cpp
#include <vector>
using namespace std;

vector<vector<int>> threeNumberSum(vector<int> array, int targetSum) {
  vector<vector<int>>res;
  sort(array.begin(),array.end());
  for(int i=0;i<array.size()-2;i++){
    int l = i+1 , r = array.size()-1;
    while(l<r){
      if(array[i] + array[l] + array[r] == targetSum){
        res.push_back({array[i],array[l],array[r]});
        l++,r--;
      }else if(array[i] + array[l] + array[r] > targetSum){
        r--;
      }else{
        l++;
      }
    }
  }
  return res;
}
```
### Smallest Difference

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

vector<int> smallestDifference(vector<int> arrayOne, vector<int> arrayTwo) {
  sort(arrayOne.begin(),arrayOne.end());
  sort(arrayTwo.begin(),arrayTwo.end());
  int l1=0,l2=0;
  vector<int> ans = {0,0};
  int minDiff = INT_MAX;
  while(l1 < arrayOne.size() and l2 < arrayTwo.size()){
    if(abs(arrayOne[l1]-arrayTwo[l2]) < minDiff){
      ans[0] = arrayOne[l1];
      ans[1] = arrayTwo[l2];
      minDiff = abs(arrayOne[l1]-arrayTwo[l2]);
    }
    if(arrayOne[l1] == arrayTwo[l2])
      return ans;
    else if(arrayOne[l1]<arrayTwo[l2])
      l1++;
    else
      l2++;
  }
  return ans;
}
```
### Move Element To End

#### - CPP Solution
```cpp
#include <vector>

using namespace std;

vector<int> moveElementToEnd(vector<int> array, int toMove) {
  int l=0,r=array.size()-1;
  while(l<r){
    while(l<r && array[r] == toMove)
      r--;
    if(array[l] == toMove){
      swap(array[l],array[r]);
      r--;
    }
    l++;
  }
  return array;
}
```
### Monotonic Array

#### - CPP Solution
```cpp
using namespace std;

bool isMonotonic(vector<int> array) {
  if(array.size() <= 2)
    return true;
  int direction = array[1] - array[0];
  for(int i=2;i<array.size();i++){
    if(direction == 0){
      direction = array[i]-array[i-1];
      continue;
    }
    if((direction < 0 and array[i-1] < array[i]) or 
       (direction > 0 and array[i-1] > array[i]))
        return false;
  }
  return true;
}
```
### Spiral Traverse

#### - CPP Solution
```cpp
using namespace std;

vector<int> spiralTraverse(vector<vector<int>> array) {
  vector<int> res;
  int L = 0, R = array[0].size(),T = 0, B = array.size();
  while(L<R and T<B){
    for(int i = L;i<R;i++)
      res.push_back(array[T][i]);
    T++;
    for(int i=T;i<B;i++)
      res.push_back(array[i][R-1]);
    R--;
    if(!(L<R and T<B)){
      break;
    }
    for(int i = R-1;i>=L;i--)
      res.push_back(array[B-1][i]);
    B--;
    for(int i=B-1;i>=T;i--)
      res.push_back(array[i][L]);
    L++;
  }
  return res;
}
```
### Longest Peak

#### - CPP Solution
```cpp
using namespace std;

int longestPeak(vector<int> array) {
  int longestPeakList = 0;
  int i = 1;
  while(i < int(array.size()-1)){
    bool isPeak = array[i-1]<array[i] and array[i]>array[i+1];
    if(!isPeak){
      i++;
      continue;
    }
    int left = i-2;
    while(left >= 0 and array[left] < array[left+1]){
      left--;
    }
    int right = i+2;
    while(right < array.size() and array[right] < array[right-1]){
      right++;
    }
    longestPeakList = max(longestPeakList,right-left-1);
    i = right;
  }
  return longestPeakList;
}
```
### Array Of Products

#### - CPP Solution
```cpp
#include <vector>

using namespace std;

vector<int> arrayOfProducts(vector<int> array) {
  vector<int> res(array.size(),0);
  int prod = 1;
  for(int i=0;i<array.size();i++){
    res[i] = prod;
    prod*=array[i];
  }
  prod = 1;
  for(int i=array.size()-1;i>=0;i--){
    res[i] *= prod;
    prod*=array[i];
  }
  return res;
}
```
### First Duplicate Value

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

int firstDuplicateValue(vector<int> array) {
  for(int i=0;i<array.size();i++){
    int ind = abs(array[i]);
    if(array[ind-1] < 0)
      return ind;
    array[ind-1] *=-1;
  }
  return -1;
}
```
### Merge Overlapping Intervals

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

vector<vector<int>> mergeOverlappingIntervals(vector<vector<int>> intervals) {
  sort(intervals.begin(),intervals.end());
  vector<vector<int>> ans;
  for(int i=0;i<intervals.size();){
    vector<int> interval = intervals[i];
    i++;
    while(i<intervals.size()){
      // overlap
      if(intervals[i][0] >= interval[0]  and intervals[i][0] <= interval[1]){
        interval[1] = max(interval[1],intervals[i][1]);
        i++;
        continue;
      }
      break;
    }
    ans.push_back(interval);
  }
  return ans;
}
```
### Best Seat

#### - CPP Solution
```cpp
using namespace std;

int bestSeat(vector<int> seats) {
  int l=0,r=seats.size()-1,resIndx = -1,maxDis=0;
  while(l<r){
    if(!seats[l]){
      int s=l,e=l;
      l++;
      while(l<r and !seats[l])
        e=l++;
      if(resIndx==-1 or maxDis<e-s){
        resIndx = (e+s)/2;
        maxDis = e-s;
      }
    }else
      l++;
  }
  return resIndx;
}
```
### Zero Sum Subarray

#### - CPP Solution
```cpp
using namespace std;

bool zeroSumSubarray(vector<int> nums) {
  for(int i=0;i<nums.size();i++){
    int sum = 0;
    for(int j=i;j<nums.size();j++){
      sum+=nums[j];
      if(sum == 0)
        return true;
    }
  }
  return false;
}
```

#### - Another Solution
```cpp
using namespace std;

bool zeroSumSubarray(vector<int> nums) {
  unordered_set<int> sums = {0};
  int currentSum = 0;
  for(int num:nums){
    currentSum+=num;
    if(sums.find(currentSum)!=sums.end())
      return true;
    sums.insert(currentSum);
  }
  return false;
}
```
### Missing Numbers

#### - CPP Solution
```cpp
using namespace std;

vector<int> missingNumbers(vector<int> nums) {
  sort(nums.begin(),nums.end());
  vector<int> res={(int)nums.size()+1,(int)nums.size()+2};
  int ind = 0,curr = 1,l=0;
  while(l<nums.size()){
    if(nums[l] != curr){
      res[ind++] = curr;
      curr++;
      continue;
    }
    l++;
    curr++;
      
  }
  return res;
}
```

#### - Another Solution
```cpp
using namespace std;

vector<int> missingNumbers(vector<int> nums) {
  int n = nums.size() + 2;
  int totalSum = 0;
  int targetSum = n*(n+1)/2;
  for(int num:nums){
    totalSum+=num;
  }
  int avg = (targetSum-totalSum)/2;
  int targetL=avg*(avg+1)/2;
  int targetR=targetSum-targetL;
  int totalL=0,totalR=0;
  for(int num:nums){
    if(num<=avg)
      totalL+=num;
    else
      totalR+=num;
  }
  return {targetL-totalL,targetR-totalR};
}
```
### Majority Element

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public int majorityElement(int[] array) {
    int res = array[0];
    int cnt = 1;
    for(int i=1;i<array.length;i++){
      if(array[i] == res){
        cnt++;
      }else{
        if(cnt == 0){
          cnt++;
          res = array[i];
        }else{
          cnt--;
        }
      }
    }
    return res;
  }
}
```

#### - Another Solution
```java
import java.util.*;

class Program {
  public int majorityElement(int[] array) {
    int answer = 0;
    for(int i=0;i<32;i++){
      int currentValue = 1<<i;
      int onesCnt = 0;
      for(int j=0;j<array.length;j++)
        if((currentValue & array[j]) != 0)
          onesCnt++;
      if(onesCnt > array.length/2)
        answer += currentValue;
    }
    return answer;
  }
}
```
### Sweet And Savory

#### - JAVA Solution
```java
import java.util.*;

class Program {

  public int[] sweetAndSavory(int[] dishes, int target) {
    Arrays.sort(dishes);
    int l=0,r=dishes.length-1;
    int res [] = {0,0};
    if(r<1 || dishes[0]>0 ||dishes[r] <0)
      return res;
    while(l<r && dishes[l]<0 && dishes[r]>0){
      if( dishes[l] + dishes[r] <= target && (res[0] == 0 ||
        Math.abs(target - (dishes[l] + dishes[r])) < 
        Math.abs(target - (res[0] + res[1])))){
          res[0] = dishes[l];
          res[1] = dishes[r];
        }
      if(dishes[l] + dishes[r] == target)
        break;
      if(dishes[l] + dishes[r] < target){
        l++;
      }else{
        r--;
      }    
    }
    return res;
  }
}
```

### Four Number Sum

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

vector<vector<int>> fourNumberSum(vector<int> array, int targetSum) {
  vector<vector<int>> ans;
  sort(array.begin(),array.end());
  for(int i=0;i<array.size()-3;i++){
    for(int j=i+1;j<array.size()-2;j++){
      int l=j+1,r=array.size()-1;
      int remain = targetSum -array[i]-array[j];
      while(l<r){
         if(remain == array[l]+array[r]){
           ans.push_back({array[i],array[j],array[l],array[r]});
           l++;
           r--;
         }else if(remain > array[l]+array[r]){
           l++;
        }else{
           r--;
        }
      }
    }
  }
return ans;  
}
```

### Subarray Sort

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int[] subarraySort(int[] array) {
        // Write your code here.
        int st=-1,end = -1,n=array.length;
        for(int i=0;i<n-1;i++){
            if(array[i]>array[i+1]){
                st = i;
                break;
            }
        }
        if(st != -1){
            for(int i=n-1;i>st;i--){
                if(array[i]<array[i-1]){
                    end = i;
                    break;
                }
            }
            if(end == -1)
                end = n-1;
            int mn = Integer.MAX_VALUE;
            for(int i=st;i<=end;i++){
                mn = Math.min(mn,array[i]);
            }
            for(int i=0;i<end;i++){
                if(array[i]>mn){
                    st = i;
                    break;
                }
            }
            int mx = Integer.MIN_VALUE;
            for(int i=st;i<=end;i++){
                mx = Math.max(mx,array[i]);
            }
            for(int i=end;i<n;i++){
                if(array[i]<mx){
                    end = i;
                }
            }

        }
        return new int[] {st,end};
    }
}
```

#### - Another Solution
```java
import java.util.*;

class Program {
    public static int[] subarraySort(int[] array) {
        // Write your code here.
        int mnOutOfOrder = Integer.MAX_VALUE;
        int mxOutOfOrder = Integer.MIN_VALUE;
        for(int i=0;i<array.length;i++){
            if(isOutOfOrder(i,array)){
                mnOutOfOrder = Math.min(mnOutOfOrder,array[i]);
                mxOutOfOrder = Math.max( mxOutOfOrder, array[i]);
            }
        }
        if(mnOutOfOrder == Integer.MAX_VALUE)
            return new int[]{-1,-1};
        int leftIndex =0,rightIndex=array.length-1;
        while (array[leftIndex] <= mnOutOfOrder)
            leftIndex++;
        while (array[rightIndex] >= mxOutOfOrder)
            rightIndex--;
        return new int[] {leftIndex,rightIndex};
    }

    private static boolean isOutOfOrder(int i, int[] array) {
        if(i == array.length-1)
            return array[i] < array[i-1];
        if(i == 0)
            return array[i] > array[i+1];
        return array[i] < array[i-1] || array[i] > array[i+1];
    }
}
```
### Largest Range

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

vector<int> largestRange(vector<int> a) {
  sort(a.begin(),a.end());
  int l=0;
  vector<int> ans = {0,0};
  while(l<a.size()){
    int st = l;
    int e = l;
    if(l+1<a.size() and abs(a[l] - a[l+1]) <= 1){
      while(l+1<a.size() and abs(a[l] - a[l+1]) <= 1){
        e = l+1;
        l++;
      }
    }else
      l++;
    if(a[ans[1]]-a[ans[0]] < a[e]-a[st]){
      //cout<<st<<" "<<e<<endl;
      ans[0]=st;
      ans[1]=e;
    }
  }
  return {a[ans[0]],a[ans[1]]};
}
```

#### - Another Solution
```cpp
#include <vector>
using namespace std;

vector<int> largestRange(vector<int> array) {
  unordered_map<int,bool>m;
  vector<int> ans = {0,0};
  for(auto num:array)
    m[num] = true;
  for(int num:array){
    if(!m[num])
      continue;
    m[num] = false;
    int left = num-1;
    int right = num+1;
    while(m[left]){
      m[left] = false;
      left--;
    }
    while(m[right]){
      m[right] = false;
      right++;
    }
    if(ans[1]-ans[0] <= right-left-2){
      ans[0] = left+1;
      ans[1] = right-1;
    }
  }
  return ans;
}
```

### Min Rewards

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int minRewards(int[] scores) {
        // Write your code here.
        int [] rewards = new int[scores.length];
        int ans = 0;
        Arrays.fill(rewards,1);
        for(int i=1;i<scores.length;i++){
            if(scores[i]>scores[i-1])
                rewards[i] = rewards[i-1]+1;
            else{
                for(int j=i-1;j>=0&&scores[j]>scores[j+1];j--){
                    rewards[j]=Math.max(rewards[j+1]+1,rewards[j]);
                }
            }
        }
        for(int i=0;i<rewards.length;i++)
            ans+=rewards[i];
        return ans;
    }
}
```

#### - Another Solution
```java
import java.util.*;

class Program {
  public static int minRewards(int[] scores) {
    int [] rewards = new int[scores.length];
    int ans = 0;
    Arrays.fill(rewards,1);
    // Write your code here.
    for(int i=1;i<scores.length;i++)
      if(scores[i] > scores[i-1])
        rewards[i] = rewards[i-1]+1;
    for(int i=scores.length-2;i>=0;i--)
      if(scores[i] > scores[i+1])
        rewards[i] = Math.max(rewards[i+1]+1,rewards[i]);
    for(int i=0;i<rewards.length;i++)
        ans+=rewards[i];
    return ans;
  }
}
```

### Zigzag Traverse

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static List<Integer> zigzagTraverse(List<List<Integer>> array) {
        // Write your code here.
        int c=0,r=0,width = array.get(0).size()-1,height = array.size()-1;
        List<Integer> ans = new ArrayList<>();
        boolean isGoingDown = true;
        while (!isOutOfBound(r,c,height,width)){
            ans.add(array.get(r).get(c));
            if(isGoingDown){
                if(c == 0 || r == height){
                    isGoingDown = false;
                    if(r == height){
                        c++;
                    }else{
                        r++;
                    }
                }else{
                    r++;
                    c--;
                }
            }else{
                if(r == 0 || c == width){
                    isGoingDown = true;
                    if(c == width){
                        r++;
                    }else{
                        c++;
                    }
                }else{
                    r--;
                    c++;
                }
            }
        }
        return ans;
    }

    private static boolean isOutOfBound(int r, int c, int height, int width) {
        return r<0 || c <0 || r>height || c>width;
    }
}
```
### Longest Subarray With Sum

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public int[] longestSubarrayWithSum(int[] array, int targetSum) {
        // Write your code here.
        int st = 0,e = 0,n=array.length,currSum=-1,resSt=-1,resEnd=-1;
        boolean foundSolution = false;
        while (st<n && e<n){
            if(currSum < targetSum || foundSolution){
                foundSolution = false;
                if(currSum == -1)
                    currSum = 0;
                currSum+=array[e];
                e++;
            }
            else if(currSum > targetSum){
                currSum-=array[st];
                st++;
            }
            else {
                foundSolution = true;
                if(resSt == -1 || e-st > resEnd-resSt){
                    resSt = st;
                    resEnd = e;
                }
            }
        }
        if(currSum == targetSum && (resSt == -1 || e-st > resEnd-resSt)){
            resSt = st;
            resEnd = e;
        }
        return resSt == -1? new int[] {}: new int[] {resSt,resEnd-1};
    }
}
```

### knight Connection

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public int knightConnection(int[] knightA, int[] knightB) {
        // Write your code here.
        if(knightA[0] == knightB[0] && knightA[1] == knightB[1])
            return 0;
        int [][] possiblePosition = new int [][]{{-2,1},{-2,-1},{2,1},{2,-1},{-1,2},{-1,-2},{1,2},{1,-2}};
        int depth = 0;
        Queue<int[]> queue = new LinkedList<>();
        queue.add(knightA);
        Set<String> visited = new HashSet<>();
        while (!queue.isEmpty()){
            int sz = queue.size();
            depth++;
            while (sz>0){
                int[] curr = queue.remove();
                for(int i=0;i<possiblePosition.length;i++){
                    int newX = curr[0]+possiblePosition[i][0];
                    int newY = curr[1]+possiblePosition[i][1];
                    if(newX == knightB[0] && newY == knightB[1])
                        return (int) Math.ceil((double) depth/2);
                    if(visited.contains(newX+":"+newY))
                        continue;
                    queue.add(new int[]{newX,newY});
                    visited.add(newX+":"+newY);
                }
                sz--;

            }
        }
        return depth;
    }
}
```

### Count Squares

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public int countSquares(int[][] points) {
        // Write your code here.
        int cnt = 0;
        Set<String> pointsSet = new HashSet<>();
        for(var point:points)
            pointsSet.add(convertToString(point));
        for(var pointA:points){
            for(var pointB:points){
                if(pointA == pointB)
                    continue;
                double [] midPoint = new double[]{(double) (pointA[0] + pointB[0]) /2.0, (double) (pointA[1] + pointB[1]) /2.0};
                double disX = pointA[0] - midPoint[0];
                double disY = pointA[1] - midPoint[1];
                double [] p1 = new double[]{midPoint[0]-disY,midPoint[1]+disX};
                double [] p2 = new double[]{midPoint[0]+disY,midPoint[1]-disX};
                if(pointsSet.contains(covertDoublePoint(p1))&&pointsSet.contains(covertDoublePoint(p2)))
                    cnt++;

            }
        }
        return cnt/4;
    }

    private String covertDoublePoint(double[] point) {
        if(point[0]%1 == 0 && point[1]%1 ==0)
            return (int) point[0] + ":" + (int) point[1];
        return point[0] + ":" + point[1];
    }

    private String convertToString(int[] point) {
        return point[0] + ":" + point[1];
    }
}
```

### Minimum area rectangle

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public int minimumAreaRectangle(int[][] points) {
        int minArea = Integer.MAX_VALUE;
        Set<String> pointSet = new HashSet<>();
        // Write your code here.
        for(int i=0;i< points.length;i++)
            pointSet.add(convertPointToString(points[i]));

        for(int i=0;i< points.length;i++){
            for(int j=0;j<points.length;j++){
                if(i == j)
                    continue;
                int [] p2 = new int[]{points[i][0],points[j][1]};
                int [] p4 = new int[]{points[j][0],points[i][1]};
                if(points[i][0] < points[j][0] && points[i][1] < points[j][1]
                        && pointSet.contains(convertPointToString(p2))&&pointSet.contains(convertPointToString(p4))){
                    minArea = Math.min(minArea,calculateArea(p2[0],p4[0],p4[1],p2[1]));
                }
            }
        }
        return minArea == Integer.MAX_VALUE ? 0:minArea;
    }

    private int calculateArea(int x1,int x2,int y1,int y2) {
        return Math.abs(x1-x2) * Math.abs(y1-y2);
    }

    private String convertPointToString(int[] point) {
        return Integer.toString(point[0]) + ':' + Integer.toString(point[1]);
    }
}
```
### Apartment Hunting

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int apartmentHunting(
            List<Map<String, Boolean>> blocks, String[] reqs
    ) {
        // Write your code here.
        int[] maxDistanceAtBlocks = new int[blocks.size()];
        Arrays.fill(maxDistanceAtBlocks,Integer.MIN_VALUE);
        int idx = 0;
        int mn = Integer.MAX_VALUE;
        for(int i=0;i< blocks.size();i++){
            for(int j=0;j< reqs.length;j++){
                int farestDistance = Integer.MAX_VALUE;
                for(int k=0;k< blocks.size();k++){
                    if(blocks.get(k).get(reqs[j])){
                        farestDistance = Math.min(Math.abs(i-k),farestDistance);
                    }
                }
                maxDistanceAtBlocks[i]=Math.max(maxDistanceAtBlocks[i],farestDistance);
            }
        }
        for(int i=0;i< blocks.size();i++){
            if(mn>maxDistanceAtBlocks[i]){
                idx = i;
                mn = maxDistanceAtBlocks[i];
            }
        }
        return idx;
    }
}
```

#### - Another Solution
```java
import java.util.*;

class Program {
    public static int apartmentHunting(
            List<Map<String, Boolean>> blocks, String[] reqs
    ) {
        // Write your code here.
        int[][] mnDistanceAtBlocks = new int[reqs.length][blocks.size()];
        for(int i=0;i< reqs.length;i++){
            for(int k=0;k< blocks.size();k++){
                mnDistanceAtBlocks[i][k] = Integer.MAX_VALUE;
                if(blocks.get(k).get(reqs[i])){
                    mnDistanceAtBlocks[i][k] = 0;
                }else{
                    if(k>0){
                        mnDistanceAtBlocks[i][k] = mnDistanceAtBlocks[i][k-1] == Integer.MAX_VALUE?
                                mnDistanceAtBlocks[i][k-1]:mnDistanceAtBlocks[i][k-1]+1;
                    }
                }
            }
            for(int k=blocks.size()-2;k>=0;k--){
                mnDistanceAtBlocks[i][k] = Math.min(mnDistanceAtBlocks[i][k],mnDistanceAtBlocks[i][k+1]+1);
            }
        }
        int [] maxDistanceAtBlocks = new int[blocks.size()];
        for(int j=0;j< blocks.size();j++) {
            int mxDistance = Integer.MIN_VALUE;
            for (int i = 0; i < reqs.length; i++) {
                mxDistance = Math.max(mxDistance,mnDistanceAtBlocks[i][j]);
            }
            maxDistanceAtBlocks[j] = mxDistance;
        }
        int idx = 0;
        int mn = Integer.MAX_VALUE;
        for(int i=0;i< blocks.size();i++){
            if(mn>maxDistanceAtBlocks[i]){
                idx = i;
                mn = maxDistanceAtBlocks[i];
            }
        }
        return idx;
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

### 

#### - JAVA Solution
```java
```
