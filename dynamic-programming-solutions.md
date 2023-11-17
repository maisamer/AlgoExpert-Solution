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

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public static int numberOfWaysToMakeChange(int n, int[] denoms) {
    // Write your code here.
    int [] dp = new int [n+1];
    dp[0] = 1;
    for(int i=1;i<=n;i++){
      dp[i] = 0;
    }
    for(int coin:denoms){
      for(int amount = 1;amount<=n;amount++){
          if(amount >= coin)
            dp[amount] = dp[amount]+dp[amount-coin];
        }
    }
    return dp[n];
  }
}
```
### Min Number Of Coins For Change

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int minNumberOfCoinsForChange(int n, int[] denoms) {
        // Write your code here.
        int dp [] = new int [n+1];
        Arrays.fill(dp,Integer.MAX_VALUE);
        dp[0] = 0;
        for(int coin:denoms){
            for(int amount = 1;amount<=n;amount++){
                if(amount >= coin){
                    dp[amount] = Math.min(dp[amount],dp[amount-coin] == Integer.MAX_VALUE ? Integer.MAX_VALUE : dp[amount-coin]+1);
                }
            }
        }
        return dp[n] == Integer.MAX_VALUE ? -1:dp[n];
    }
}
```
### Levenshtein Distance 

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public static int levenshteinDistance(String str1, String str2) {
    // Write your code here.
    int [][] table = new int [str1.length()+1][str2.length()+1];
    for(int i=0;i<=str1.length();i++){
      table[i][0] = i;
    } 
    for(int i=0;i<=str2.length();i++){
      table[0][i] = i;
    } 
    for(int i=1;i<=str1.length();i++){
      for(int j=1;j<=str2.length();j++){
        if(str1.charAt(i-1) == str2.charAt(j-1))
          table[i][j] = table[i-1][j-1];
        else
          table[i][j] = 1 + Math.min(table[i-1][j-1],Math.min(table[i][j-1],table[i-1][j]));
      }
    }    
    return table[str1.length()][str2.length()];
  }
}
```
### another approach

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int levenshteinDistance(String str1, String str2) {
        // Write your code here.
        int [][] table = new int [2][str2.length()+1];
        for(int i=0;i<=str2.length();i++)
            table[0][i] = i;
      
        for(int i=1;i<=str1.length();i++){
            int prevInd = i%2 == 0 ? 1 : 0;
            int currInd = i%2;
            table[currInd][0] = i;
            for(int j=1;j<=str2.length();j++){
                if(str1.charAt(i-1) == str2.charAt(j-1))
                    table[currInd][j] = table[prevInd][j-1];
                else
                    table[currInd][j] = 1 + Math.min(table[prevInd][j-1],
                                     Math.min(table[currInd][j-1],table[prevInd][j]));
            }
        }
        return table[str1.length() % 2][str2.length()];
    }
}
```

### another approach

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public static int levenshteinDistance(String str1, String str2) {
    String small = str1.length() < str2.length() ? str1 : str2;
    String big = str1.length() >= str2.length() ? str1 : str2;
    int [][] table = new int [2][small.length()+1];
    for(int i=0;i<small.length();i++)
      table[0][i] = i;
    for(int i=1;i<=big.length();i++){
      int current = i%2;
      int prev = current == 0 ? 1:0;
      table[current][0] = i;
      for(int j=1;j<=small.length();j++){
        if(small.charAt(j-1) == big.charAt(i-1))
          table[current][j] = table[prev][j-1];
        else
          table[current][j] = 1+ Math.min(table[prev][j-1],
                              Math.min(table[prev][j],table[current][j-1]));
      }
    }
    return table[big.length()%2][small.length()];
  }
}
```

### Number Of Ways To Traverse Graph

#### - JAVA Solution
```java
import java.util.*;

class Program {

  public int numberOfWaysToTraverseGraph(int width, int height) {
    int table [][] = new int [width+1][height+1];
    for(int i=1;i<width+1;i++){
      for(int j=1;j<height+1;j++){
        if(i == 1 || j == 1)
          table[i][j] = 1;
        else
          table[i][j] = table[i-1][j]+table[i][j-1];
      }
    }
    return table[width][height];
  }
}

```

### another approach

#### - JAVA Solution
```java
import java.util.*;

class Program {

  public int numberOfWaysToTraverseGraph(int width, int height) {
    int numerator = factorial(width+height-2);
    numerator = numerator / factorial(width-1);
    numerator = numerator / factorial(height-1);
    return numerator;
  }
  private int factorial(int n){
    int res = 1;
    for(int i=2;i<=n;i++)
      res*=i;
    return res;
  }
}
```

### Max Sum Increasing Subsequence

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static List<List<Integer>> maxSumIncreasingSubsequence(int[] array) {
        // Write your code here.
        int mx = Integer.MIN_VALUE;
        int mxInd = -1;
        int n = array.length;
        int [] sequence = new int[n];
        Arrays.fill(sequence,-1);
        int [] maxSums = array.clone();
        for(int i=0;i<n;i++){
            for(int j=0;j<i;j++){
                if(array[i]>array[j] && maxSums[j]+array[i]>=maxSums[i]){
                    maxSums[i] = maxSums[j] + array[i];
                    sequence[i] = j;
                }
            }
            if(maxSums[i]>=mx){
                mx = maxSums[i];
                mxInd = i;
            }
        }
        int finalMx = mx;
        int finalMxInd = mxInd;
        return new ArrayList<List<Integer>>() {
            {
                add(List.of(finalMx)); // Example max sum
                add(buildSequence(sequence,array, finalMxInd)); // Example max sequence
            }
        };
    }

    private static List<Integer> buildSequence(int[] sequence, int[] array,int curr) {
        List<Integer> res = new ArrayList<>();
        while(curr != -1){
            res.add(0,array[curr]);
            curr = sequence[curr];
        }
        return  res;
    }
}
```

### Longest Common Subsequence

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public static List<Character> longestCommonSubsequence(String str1, String str2) {
    List<List<List<Character>>> table = new ArrayList<List<List<Character>>>();
    for(int i=0;i<str1.length()+1;i++){
      table.add(new ArrayList<List<Character>>());
      for(int j=0;j<str2.length()+1;j++){
        table.get(i).add(new ArrayList<Character>());
      }
    }
    for(int i=1;i<str1.length()+1;i++){
      for(int j=1;j<str2.length()+1;j++){
        if(str1.charAt(i-1) == str2.charAt(j-1)){
          List<Character> copy = new ArrayList<>(table.get(i-1).get(j-1));
          table.get(i).set(j,copy);
          table.get(i).get(j).add(str1.charAt(i-1));
        }else{
          if(table.get(i).get(j-1).size() >= table.get(i-1).get(j).size())
            table.get(i).set(j,table.get(i).get(j-1));
          else
            table.get(i).set(j,table.get(i-1).get(j));
        }
      }
    }
    return table.get(str1.length()).get(str2.length());
  }
}
```

### another approach

#### - JAVA Solution
```java

import java.util.*;
class Program {
    public static List<Character> longestCommonSubsequence(String str1, String str2) {
        List<List<State>> lcs = new ArrayList<List<State>>();
        for(int i=0;i<str1.length()+1;i++){
            lcs.add(new ArrayList<State>());
            for(int j=0;j<str2.length()+1;j++){
                lcs.get(i).add(new State(' ',0,0,0));
            }
        }
        for(int i=1;i<str1.length()+1;i++){
            for(int j=1;j<str2.length()+1;j++){
                if(str1.charAt(i-1) == str2.charAt(j-1)){
                    State state = new State(str1.charAt(i-1),lcs.get(i-1).get(j-1).length + 1, i-1,j-1);
                    lcs.get(i).set(j,state) ;
                }else{
                    if(lcs.get(i - 1).get(j).length >= lcs.get(i).get(j-1).length){
                        State state = new State(' ',lcs.get(i-1).get(j).length, i-1,j);
                        lcs.get(i).set(j,state);
                    }else{
                        State state = new State(' ',lcs.get(i).get(j-1).length, i,j-1);
                        lcs.get(i).set(j,state);
                    }
                }
            }
        }
        return buildSubsequence(lcs);
    }

    static List<Character> buildSubsequence(List<List<State>> lcs){
        List<Character> res = new ArrayList<>();
        int i = lcs.size() -1;
        int j = lcs.get(0).size()-1;
        while(i != 0 && j != 0){
            State st = lcs.get(i).get(j);
            if(st.c != ' '){
                res.add(0, st.c);
            }
            i = st.i;
            j = st.j;
        }
        return res;
    }

    static class State{
        public Character c;
        public int length;
        public int i;
        public int j;

        public State(char c, int l, int i, int j) {
            this.c = c;
            this.length = l;
            this.i = i;
            this.j = j;
        }
    }
}
```

### MinNumber Of Jumps

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int minNumberOfJumps(int[] array) {
        // Write your code here.
        int n = array.length;
        if(n == 1)
          return 0;
        int steps = array[0];
        int mnJumps = 0;
        int maxReach = array[0];
        for(int i=1;i<n-1;i++){
            maxReach = Math.max(maxReach,i+array[i]);
            steps-=1;
            if(steps == 0){
                steps = maxReach - i;
                mnJumps+=1;
            }
        }
        return mnJumps+1;
    }
}

```

### another approach

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public static int minNumberOfJumps(int[] array) {
    // Write your code here.
    int n = array.length;
    int [] jumps = new int [n];
    Arrays.fill(jumps,Integer.MAX_VALUE);
    jumps[0] = 0;
    for(int i=1;i<n;i++){
      for(int j=0;j<i;j++){
        if(j+array[j]>=i)
          jumps[i] = Math.min(jumps[i],1+jumps[j]);
      }
    }
    return jumps[n-1];
  }
}
```

### Water Area

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int waterArea(int[] heights) {
        // Write your code here.
        int ans = 0;
        int n = heights.length;
        int maxes[] = new int [n];
        int mx = 0;
        for(int i=0;i<n;i++){
            maxes[i] = mx;
            mx = Math.max(mx,heights[i]);
        }
        mx = 0;
        for(int i=n-1;i>=0;i--){
            int minHeight = Math.min(mx,maxes[i]);
            if(minHeight > heights[i])
                ans += minHeight-heights[i];
            mx = Math.max(heights[i],mx);
        }

        return ans;
    }
}
```

### Knapsack Problem

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
int mxtotal = 0;
vector<int> sol;
void recursion(vector<vector<int>> items, int capacity,int total,
                             vector<int> finalItems,int i){
        if(capacity == 0 || i >= items.size()) {
            if (total > mxtotal) {
                mxtotal = total;
                sol = finalItems;
            }
            return;
        }
        recursion(items,capacity,total,finalItems,i+1);
        if(items[i][1] <= capacity){
            finalItems.push_back(i);
            recursion(items,capacity-items[i][1],total+items[i][0],finalItems,i+1);
            finalItems.pop_back();
        }

}

vector<vector<int>> knapsackProblem(vector<vector<int>> items, int capacity) {
    mxtotal = 0;
    sol =  {};
    recursion(items,capacity,0,{},0);
    vector<int> totalValue = {mxtotal};
    vector<vector<int>> result;
    result.push_back(totalValue);
    result.push_back(sol);
    return result;
}
```

### another approach

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

vector<vector<int>> knapsackProblem(vector<vector<int>> items, int capacity) {
  vector<int> finalResult;
  vector<vector<int>> table(items.size() + 1, vector<int> (capacity + 1));
  for(int i=1;i<table.size();i++){
    for(int j=1;j<table[i].size();j++){
      if(items[i-1][1]>j)
        table[i][j] = table[i-1][j];
      else{
        table[i][j] = max(table[i-1][j],table[i-1][j-items[i-1][1]]+items[i-1][0]);
      }
    }
  }
  int i = items.size();
  int j = capacity ;
  while(i > 0){
    if(table[i][j] == table[i-1][j]){
      i--;
    }else{
      finalResult.push_back(i-1);
      j-=items[i-1][1];
      i--;
    }
    if(j == 0)
      break;
  }
  return {
      {table[items.size()][capacity]},   // total value
      finalResult, // item indices
  };
}
```

### Disk Stacking

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static List<Integer[]> diskStacking(List<Integer[]> disks) {
        // Write your code here.
        disks.sort((disk1,disk2)->disk1[2].compareTo(disk2[2]));
        int n = disks.size();
        int [][] dp = new int [n][2];
        dp[0]= new int[]{-1, disks.get(0)[2]};
        int [] mx = new int[]{0,disks.get(0)[2]};
        for(int i=1;i<n;i++){
            dp[i] = new int[]{-1, disks.get(i)[2]};
            for(int j=0;j<i;j++){
                if(valid(disks.get(j),disks.get(i)) && dp[j][1]+disks.get(i)[2] > dp[i][1]){
                    dp[i][0] = j;
                    dp[i][1] = dp[j][1]+disks.get(i)[2];
                  System.out.println("i = " + i);
                  System.out.println("j = "+j);
                    System.out.println(dp[i][1]);
                }
            }
            if(mx[1]<dp[i][1]){
                mx[0] = i;
                mx[1] = dp[i][1];
            }
        }
        
        return buildResult(disks,dp,mx[0]);
    }

    private static List<Integer[]> buildResult(List<Integer[]> disks, int[][] dp, int ind) {
        List<Integer[]> res = new ArrayList<Integer[]>();
        while(ind != -1){
            res.add(0,disks.get(ind));
            ind = dp[ind][0];
        }
        return res;
    }

    private static boolean valid(Integer[] a, Integer[] b) {
        return a[0] < b[0] && a[1] < b[1] && a[2] < b[2];
    }
}
```

### Numbers In Pi

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
int recursion(string pi,int i,unordered_set<string> dic,vector<int> mem){
	if(i >= pi.size())
		return -1;
	if(mem[i] != INT_MAX)
		return mem[i];
	int ans = INT_MAX;
	for(int j = i;j<pi.size();j++){
		string sub = pi.substr(i,j-i+1);
		if(dic.find(sub) != dic.end()){
			int op1 = recursion(pi,j+1,dic,mem);
			if(op1 != INT_MAX)
				op1++;
			ans = min(op1,ans);
		}
	}
    return mem[i] = ans;
}
int numbersInPi(string pi, vector<string> numbers) {
  vector<int> mem(pi.size(),INT_MAX);
	unordered_set<string> dic;
	for(string word:numbers)
		dic.insert(word);
  int res = recursion(pi,0,dic,mem);
  return res == INT_MAX ? -1 : res;
}
```

### Maximum Sum Submatrix

#### - JAVA Solution
```java
import java.util.*;

class Program {

    public int maximumSumSubmatrix(int[][] matrix, int size) {
        // Write your code here.
        int mx = Integer.MIN_VALUE;
        int n = matrix.length;
        int m = matrix[0].length;
        for(int i=1;i<n;i++)
            matrix[i][0] = matrix[i-1][0] + matrix[i][0];
        for(int i=1;i<m;i++)
            matrix[0][i] = matrix[0][i-1] + matrix[0][i];
        for(int i=1;i<n;i++){
            for(int j=1;j<m;j++){
                matrix[i][j] = matrix[i][j-1] + matrix[i][j] + matrix[i-1][j] - matrix[i-1][j-1];
            }
        }
        for(int i=size-1;i<n;i++){
            for(int j=size-1;j<m;j++){
                int subSum = matrix[i][j];
                if(i-size >=0)
                    subSum-=matrix[i-size][j];
                if(j-size>=0)
                    subSum-=matrix[i][j-size];
                if(j-size>=0 && i-size>=0)
                    subSum+=matrix[i-size][j-size];
                mx = Math.max(mx,subSum);
            }
        }
        return mx;
    }
}
```

### Maximize Expression

#### - JAVA Solution
```java
import java.util.*;

class Program {

    public int maximizeExpression(int[] array) {
        // Write your code here.
        if(array.length < 4)
            return 0;
        int mx = Integer.MIN_VALUE;
        for(int i=0;i< array.length;i++){
            for(int j=i+1;j< array.length;j++){
                for(int k=j+1;k< array.length;k++){
                    for(int m=k+1;m< array.length;m++){
                        mx = Math.max(mx,array[i]-array[j]+array[k]-array[m]);
                    }
                }
            }
        }
        return  mx;
    }
}
```

### another approach

#### - JAVA Solution
```java
import java.util.*;

class Program {

    public int maximizeExpression(int[] array) {
        // Write your code here.
        if(array.length < 4)
            return 0;
        int [] a =new int[array.length];
        int [] ab =new int[array.length];
        int [] abc =new int[array.length];
        int [] abcd =new int[array.length];
        a[0] = array[0];
        ab[0] = Integer.MIN_VALUE;
        abc[1] = Integer.MIN_VALUE;
        abcd[2] = Integer.MIN_VALUE;
        // get max a
        for(int i=1;i<array.length;i++)
            a[i] = Math.max(a[i-1],array[i]);
        for(int i=1;i<array.length;i++)
            ab[i] = Math.max(ab[i-1],a[i-1]-array[i]);
        for(int i=2;i<array.length;i++)
            abc[i] = Math.max(abc[i-1],ab[i-1]+array[i]);
        for(int i=3;i<array.length;i++)
            abcd[i] = Math.max(abcd[i-1],abc[i-1]-array[i]);
        return abcd[array.length-1];
    }
}
```

### another approach

#### - JAVA Solution
```java
import java.util.*;

class Program {

    public int maximizeExpression(int[] array) {
        // Write your code here.
        if(array.length < 4)
            return 0;
        int [] dp =new int[]{array[0],array[0]-array[1],array[0]-array[1]+array[2],array[0]-array[1]+array[2]-array[3]};
        for(int i=0;i<array.length;i++){
            if(i>2)
                dp[3] = Math.max(dp[3],dp[2]-array[i]);
            if(i>1)
                dp[2] = Math.max(dp[2],dp[1]+array[i]);
            if(i>0)
                dp[1] = Math.max(dp[1],dp[0]-array[i]);
            dp[0] = Math.max(dp[0],array[i]);
        }
        return  dp[3];
    }
}
```

### Dice Throws

#### - JAVA Solution
```java
import java.util.Arrays;

class Program {
    public int diceThrows(int numDice, int numSides, int target) {
        if(numDice*numSides < target)
            return 0;
        Integer [][] mem = new Integer[numDice+1][target+1];
        return getPermutationCountForTargetSum(numDice,numSides,target,mem);
    }

    private int getPermutationCountForTargetSum(int numDice, int numSides, int target, Integer[][] mem) {
        if(numDice < 0)
            return 0;
        if(target == 0){
            if(numDice ==0)
                return 1;
            return 0;
        }
        if(mem[numDice][target] != null)
            return mem[numDice][target];
        int ans = 0;
        for(int i = 1;i<=numSides && target - i >= 0;i++){
            ans+=getPermutationCountForTargetSum(numDice -1 ,numSides,target-i, mem);
        }
        return mem[numDice][target] = ans;
    }
}
```

### another approach

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public int diceThrows(int numDice, int numSides, int target) {
    // Write your code here.
    int [][] table = new int[2][target+1];
    table[0][0]=1;
    for(int i=1;i<=numDice;i++){
      for(int j=0;j<=target;j++){
        int sum =0;
        for(int k=1;k<=numSides && j-k >=0;k++){
          sum+=table[i%2==0?1:0][j-k];
        }
        table[i%2][j]=sum;
      }
        
    }
    return table[numDice%2][target];
  }
}
```

### another approach

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public int diceThrows(int numDice, int numSides, int target) {
    // Write your code here.
    int [][] table = new int[numDice+1][target+1];
    for(int i=0;i<=target;i++)
      table[0][i]= i==0?1:0;
    for(int i=1;i<=numDice;i++){
      for(int j=1;j<=target;j++){
        for(int k=1;k<=numSides && j-k >=0;k++){
          table[i][j]+=table[i-1][j-k];
        }
      }
    }
    return table[numDice][target];
  }
}
```

### Juice Bottling

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public ArrayList<Integer> juiceBottling(int[] prices) {
        // Write your code here.
        int n = prices.length-1;
        ArrayList<Integer> ans = new ArrayList<>();
        int [] dp = new int[n+1];
        int [] sequence = new int[n+1];
        Arrays.fill(dp,Integer.MIN_VALUE);
        dp[0] = 0;
        for(int i=1;i<=n;i++){
            for (int j=1;j<=i;j++){
                if(dp[i] < dp[i-j]+prices[j]) {
                    dp[i] = dp[i - j] + prices[j];
                    sequence[i] = j;
                }
            }
        }
        while(n>0){
            System.out.println(sequence[n]);
            ans.add(sequence[n]);
            n-=sequence[n];
        }
        return ans;
    }
}
```

### Max Profit With K Transactions

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int maxProfitWithKTransactions(int[] prices, int k) {
        // Write your code here.
        if(prices.length < 1)
            return 0;
        int [][] profits = new int[k+1][prices.length];
        for(int t=1;t<=k;t++){
           int mxProfit = Integer.MIN_VALUE;
            for(int d=1;d<prices.length;d++){
                mxProfit = Math.max(mxProfit,profits[t-1][d-1]-prices[d-1]);
                profits[t][d] = Math.max(profits[t][d-1],mxProfit+prices[d]);
            }
        }
        return profits[k][prices.length-1];
    }
}
```

### Palindrome Partitioning Min Cuts

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static int palindromePartitioningMinCuts(String str) {
        Integer [][] mem = new Integer[str.length()][str.length()];
        return palindromePartitioningHelper(str,0,0,mem);
    }
    public static int palindromePartitioningHelper(String str,int l,int r,Integer [][] mem) {
        // Write your code here.
        if(l >= str.length() && r >= str.length())
            return -1;
        if(r >= str.length() || l >= str.length())
            return Integer.MAX_VALUE;
        if(mem[l][r] != null)
          return mem[l][r];
        int res1 = Integer.MAX_VALUE , res2;
        if(isPalindrome(str.substring(l,r+1))){
            res1 = palindromePartitioningHelper(str,r+1,r+1,mem);
            if(res1 != Integer.MAX_VALUE)
                res1++;
        }
        res2 = palindromePartitioningHelper(str,l,r+1,mem);
        return mem[l][r] = Math.min(res2,res1);
    }
    static boolean isPalindrome(String str){
        int l = 0;
        int r = str.length()-1;
        while (l<r){
            if(str.charAt(l) != str.charAt(r))
                return false;
            l++;
            r--;
        }
        return true;
    }
}
```

### another approach

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public static int palindromePartitioningMinCuts(String str) {
    // Write your code here.
    int n = str.length();
    Boolean [][] palindromes = new Boolean[n][n];
    Integer [] cuts = new Integer[n];
    for(int i=0;i<n;i++)
      for(int j=i;j<n;j++)
        palindromes[i][j] = isPalindrome(str.substring(i,j+1));
    for(int i=0;i<n;i++)
      if(palindromes[0][i])
        cuts[i] = 0;
      else{
        cuts[i] = cuts[i-1]+1;
        for(int j=1;j<i;j++)
          if(palindromes[j][i])
            cuts[i] = Math.min(cuts[i],cuts[j-1]+1);
      }
    return cuts[n-1];
  }
  static Boolean isPalindrome(String str){
      int l = 0;
      int r = str.length()-1;
      while (l<r){
          if(str.charAt(l) != str.charAt(r))
              return false;
          l++;
          r--;
      }
      return true;
    }
}
```

### another approach

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public static int palindromePartitioningMinCuts(String str) {
    // Write your code here.
    int n = str.length();
    Boolean [][] palindromes = new Boolean[n][n];
    Integer [] cuts = new Integer[n];
    for(int i=0;i<n;i++)
      palindromes[i][i] = true;
    for(int len=2;len<n+1;len++)
      for(int i=0;i<n-len+1;i++){
        int j = i+len-1;
        if(len == 2)
          palindromes[i][j] = str.charAt(i) == str.charAt(j);
        else
          palindromes[i][j] = str.charAt(i) == str.charAt(j) && palindromes[i+1][j-1];
      }
    
    for(int i=0;i<n;i++)
      if(palindromes[0][i])
        cuts[i] = 0;
      else{
        cuts[i] = cuts[i-1]+1;
        for(int j=1;j<i;j++)
          if(palindromes[j][i])
            cuts[i] = Math.min(cuts[i],cuts[j-1]+1);
      }
    return cuts[n-1];
  }
}
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

### Square Of Zeroes

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static boolean squareOfZeroes(List<List<Integer>> matrix) {
        // Write your code here.
        int n = matrix.size();
        for(int len=2;len<=n;len++){
            for(int r=0;r<n-len+1;r++){
                for(int c=0;c<n-len+1;c++){
                    boolean oneExist = false;
                    for(int j=r;j<r+len&&!oneExist;j++)
                        if(matrix.get(j).get(c) == 1)
                            oneExist = true;
                    for(int j=r;j<r+len&&!oneExist;j++)
                        if(matrix.get(j).get(c+len-1) == 1)
                            oneExist = true;
                    for(int j=c;j<c+len&&!oneExist;j++)
                        if(matrix.get(r).get(j) == 1)
                            oneExist = true;
                    for(int j=c;j<c+len&&!oneExist;j++)
                        if(matrix.get(r+len-1).get(j) == 1)
                            oneExist = true;
                    if(!oneExist)
                        return true;
                }
            }
        }
        return false;
    }
}
```

### 

#### - JAVA Solution
```java
```
