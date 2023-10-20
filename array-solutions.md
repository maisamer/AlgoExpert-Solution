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
