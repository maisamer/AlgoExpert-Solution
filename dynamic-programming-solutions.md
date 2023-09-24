## AlgoExpert DP Problems

### Max Subset Sum No Adjacent

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
unordered_map<string,int> m;
int rec(vector<int> array,int i,int sum){
  if(i>=array.size())
    return sum;
  string key = to_string(sum) + ":" + to_string(i);
  if(m[key])
   return m[key]; 
  return m[key] = max(rec(array,i+1,sum),rec(array,i+2,sum+array[i]));
}
int maxSubsetSumNoAdjacent(vector<int> array) {
  if(!array.size())
    return 0;
  m = {};
  return rec(array,0,0);
}
```
#### - another approach in java 
```java
import java.util.*;

class Program {
    public static int maxSubsetSumNoAdjacent(int[] array) {
        // Write your code here.
        if(array.length == 1)
            return array[0];
        if(array.length == 0)
            return 0;
        int second = array[0];
        int first = Math.max(array[1],second);
        for(int i=2;i<array.length;i++){
            int current = Math.max(first,second+array[i]);
            second = first;
            first = current;
        }
        return first;
    }
}
```

### Number Of Ways To Make Change

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

int numberOfWaysToMakeChange(int n, vector<int> denoms) {
  vector<int> dp(n+1,0);
  dp[0] = 1;
  for(int i=0;i<denoms.size();i++){
    for(int j=1;j<=n;j++){
      int ind = j - denoms[i];
      if(ind >= 0){
        dp[j] += dp[ind];
      }
    }
  }
  return dp[n];
}
```
### Min Number Of Coins For Change

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

int minNumberOfCoinsForChange(int n, vector<int> denoms) {
  vector<int> dp(n+1,INT_MAX-1);
  dp[0] = 0;
  for(int coin : denoms){
    for(int i=1;i<=n;i++){
      if(i>=coin){
        dp[i] = min(dp[i],1+dp[i-coin]);
      }
    }
  }
  return dp[n] == INT_MAX-1 ? -1 : dp[n];
}
```
### 

#### - CPP Solution
```cpp

```
### 

#### - CPP Solution
```cpp

```
### longest Increasing Subsequence

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static List<Integer> longestIncreasingSubsequence(int[] array) {
        // Write your code here.
        int n = array.length;
        int [] longSequence = new int[n];
        Arrays.fill(longSequence,1);
        int [] sequence = new int[n];
        Arrays.fill(sequence,-1);
        int ind = 0;
        int mx = 1;
        for(int i=1;i<n;i++){
            for(int j=0;j<i;j++){
                if(array[i]>array[j] && longSequence[i]<=longSequence[j]+1){
                    longSequence[i] = longSequence[j]+1;
                    sequence[i] = j;
                    if(mx < longSequence[i]){
                        mx = longSequence[i];
                        ind = i;
                    }
                }
            }
        }
        List<Integer> ans = new ArrayList<>();
        while(ind != -1){
            ans.add(0,array[ind]);
            ind = sequence[ind];
        }
        return ans;
    }
}
```
