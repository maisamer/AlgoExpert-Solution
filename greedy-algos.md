## AlgoExpert Greedy-algo Problems

### Minimum Waiting Time

#### - CPP Solution
```cpp
using namespace std;

int minimumWaitingTime(vector<int> queries) {
  // Write your code here.
  sort(queries.begin(),queries.end());
  int ans = 0;
  int n = queries.size();
  for(int i=0;i<n;i++)
    ans += queries[i] * (n-i-1);
  return ans;
}
```
### Class Photos

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

bool classPhotos(vector<int> redShirtHeights, vector<int> blueShirtHeights) {
  sort(redShirtHeights.begin(),redShirtHeights.end());
  sort(blueShirtHeights.begin(),blueShirtHeights.end());
  bool stRed = false;
  if(redShirtHeights[0] < blueShirtHeights[0])
    stRed = true;
  else if(redShirtHeights[0] == blueShirtHeights[0])
    return false;
  for(int i=0;i<redShirtHeights.size();i++){
    if(redShirtHeights[i] == blueShirtHeights[i])
      return false;
    if(stRed){
      if(redShirtHeights[i] > blueShirtHeights[i])
        return false;
    }else{
      if(redShirtHeights[i] < blueShirtHeights[i])
        return false;
    }
  }
  return true;
}
```

### Tandem Bicycle

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

int tandemBicycle(vector<int> redShirtSpeeds, vector<int> blueShirtSpeeds,
                  bool fastest) {
  int totalSpeed=0;
  sort(redShirtSpeeds.begin(),redShirtSpeeds.end());
  sort(blueShirtSpeeds.begin(),blueShirtSpeeds.end());
  if(fastest)
    reverse(blueShirtSpeeds.begin(),blueShirtSpeeds.end());
  for(int i=0;i<blueShirtSpeeds.size();i++){
    totalSpeed+=max(blueShirtSpeeds[i],redShirtSpeeds[i]);
  }
  return totalSpeed;
}

```
### Optimal Freelancing

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public int optimalFreelancing(Map<String, Integer>[] jobs) {
        // Write your code here.
        Arrays.sort(jobs, new Comparator<Map<String, Integer>>() {
            @Override
            public int compare(Map<String, Integer> o1, Map<String, Integer> o2) {
                return o2.get("payment").compareTo(o1.get("payment"));
            }
        });
        int ans = 0;
        boolean taken [] = new boolean[8];
        for(Map<String,Integer> job:jobs){
            int time = Math.min(job.get("deadline"),7);
            for(int i=time;i>0;i--){
                if(!taken[i]){
                    taken[i] = true;
                    ans+= job.get("payment");
                    break;
                }
            }
        }
        return ans;
    }
}
```
### Task Assignment

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public ArrayList<ArrayList<Integer>> taskAssignment(
            int k, ArrayList<Integer> tasks
    ) {
        ArrayList<ArrayList<Integer>> tasksWithIndies = new ArrayList<>();
        // Write your code here.
        for(int i=0;i<tasks.size();i++){
            ArrayList<Integer> item = new ArrayList<>();
            item.add(i);
            item.add(tasks.get(i));
            tasksWithIndies.add(item);
        }
        Collections.sort(tasksWithIndies, Comparator.comparingInt((ArrayList<Integer> o) -> o.get(1)));
        int l=0,r=tasks.size()-1;
        ArrayList<ArrayList<Integer>> ans =new ArrayList<ArrayList<Integer>>();
        while(l<r){
            ArrayList<Integer> workerTasks = new ArrayList<>();
            workerTasks.add(tasksWithIndies.get(l).get(0));
            workerTasks.add(tasksWithIndies.get(r).get(0));
            ans.add(workerTasks);
            l++;
            r--;
        }
        return ans;
    }
}
```
### 

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public int validStartingCity(int[] distances, int[] fuel, int mpg) {
    // Write your code here.
    for(int i=0;i<fuel.length;i++){
      int start = 0;
      boolean invalid = false;
      for(int j=i;j<fuel.length;j++){
        start +=(fuel[j]*mpg);
        start-=distances[j];
        if(start < 0){
          invalid = true;
          break;
        }
      }
      for(int k=0;k<i-1;k++){
        start+=(fuel[k]*mpg);
        start-=distances[k];
        if(start < 0){
          invalid = true;
          break;
        }
      }
      if(!invalid)
        return i;
    }
    return -1;
  }
}
```
### another approach

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public int validStartingCity(int[] distances, int[] fuel, int mpg) {
    // Write your code here.
    int start = 0;
    int mn = 0;
    int ind =0;
    for(int i=1;i<fuel.length;i++){
      start += fuel[i-1]*mpg - distances[i-1];
      if(start < mn){
        mn = start;
        ind = i;
      }
    }
    return ind;
  }
}
```
