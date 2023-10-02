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
### dijkstras Algorithm

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
tuple<int,int> getVertixWithMinDistance(vector<int> minDistance,unordered_set<int> visited){
  int minDis = INT_MAX;
  int vertix = 0;
  for(int i=0;i<minDistance.size();i++){
    if(visited.find(i) != visited.end())
      continue;
    if(minDistance[i]<=minDis){
      minDis = minDistance[i];
      vertix = i;
    }
  }
  return {minDis,vertix};
}

vector<int> dijkstrasAlgorithm(int start, vector<vector<vector<int>>> edges) {
  unordered_set<int> visited;
  int vertices = edges.size();
  vector<int> minDistance(vertices,INT_MAX);
  minDistance[start] = 0;
  while(visited.size() != vertices){
    auto [currentMinDistance,vertix] = getVertixWithMinDistance(minDistance,visited);
    if(currentMinDistance == INT_MAX)
      break;
    visited.insert(vertix);
    for(auto edge:edges[vertix]){
      if(visited.find(edge[0]) != visited.end())
        continue;
      minDistance[edge[0]] = min(minDistance[edge[0]],edge[1]+currentMinDistance);
    }
    
  }
  for(int i=0;i<vertices;i++)
    if(minDistance[i]==INT_MAX)
      minDistance[i] = -1;
  return minDistance;
}
```
### topological Sort

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
class Node{
public:
  int job;
  vector<Node*> preq;
  bool visited;
  bool visiting;
  Node(int job){
    this->job = job;
  }
};
class JobGraph{
public:
  unordered_map<int,Node*> graph;
  JobGraph(vector<int> jobs,vector<vector<int>> deps){
    for(int job:jobs)
      graph[job] = new Node(job);
    for(auto dep:deps)
      graph[dep[1]]->preq.push_back(graph[dep[0]]);
  }

};
bool dfs(JobGraph *graph,int job,vector<int>&orderedJobs){
  if (graph->graph[job]->visited)
    return false;
  if (graph->graph[job]->visiting)
    return true;
  graph->graph[job]->visiting = true;
  for(Node *node : graph->graph[job]->preq)
    if(dfs(graph,node->job,orderedJobs))
      return true;
  graph->graph[job]->visited = true;
  graph->graph[job]->visiting = false;
  orderedJobs.push_back(job);
  return false;
}
vector<int> topologicalSort(vector<int> jobs, vector<vector<int>> deps) {
  vector<int> orderedJobs;
  JobGraph* graph = new JobGraph(jobs,deps);
  for(int job:jobs)
    if(!graph->graph[job]->visited)
      if(dfs(graph,job,orderedJobs))
        return {};
  return orderedJobs;
}
```

### kruskal's Algorithm

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public int[][][] kruskalsAlgorithm(int[][][] edges) {
        // Write your code here.
        int n = edges.length;
        ArrayList<List<Integer>> sortedEdges = new ArrayList<>();
        for(int source=0;source<n;source++)
            for(int[] edge:edges[source])
                if(source < edge[0])
                    sortedEdges.add(Arrays.asList(source,edge[0],edge[1]));
        sortedEdges.sort(Comparator.comparingInt(e -> e.get(2)));
        int[]parents = new int[n];
        int[]ranks = new int[n];
        ArrayList<ArrayList<int[]>> mst = new ArrayList<>();
        for(int i=0;i<n;i++){
            parents[i] = i;
            ranks[i] = 0;
            mst.add(new ArrayList<>());
        }
        for(List<Integer> edge:sortedEdges){
            int vertex1Root = find(edge.get(0),parents);
            int vertex2Root = find(edge.get(1),parents);
            if(vertex1Root != vertex2Root){
                mst.get(edge.get(0)).add(new int[]{edge.get(1),edge.get(2)});
                mst.get(edge.get(1)).add(new int[]{edge.get(0),edge.get(2)});
                union(vertex1Root,vertex2Root,parents,ranks);
            }
        }
        int[][][] arrayMST = new int[n][][];
        for(int i=0;i<mst.size();i++){
            arrayMST[i] = new int[mst.get(i).size()][];
            for(int j=0;j<mst.get(i).size();j++)
                arrayMST[i][j] = mst.get(i).get(j);
        }
        return arrayMST;
    }

    private int find(Integer vertex, int[] parents) {
        if(vertex != parents[vertex])
            parents[vertex] = find(parents[vertex],parents);
        return parents[vertex];
    }
    private void union(int vertex1Root, int vertex2Root, int[] parents, int[] ranks){
        if(ranks[vertex1Root] > ranks[vertex2Root])
            parents[vertex2Root] = vertex1Root;
        else if (ranks[vertex2Root] >ranks[vertex1Root])
            parents[vertex1Root] = vertex2Root;
        else{
            parents[vertex1Root] = vertex2Root;
            ranks[vertex2Root]+=1;
        }
    }
}
```
### knuth Morris Pratt Algorithm

#### - JAVA Solution
```java
import java.util.*;

class Program {
    // O(N + M) time and O(M) space
    public static boolean knuthMorrisPrattAlgorithm(
            String string, String substring
    ) {
        // Write your code here.
        int [] pattern = buildPattern(substring);
        return matchString(string,substring,pattern);
    }

    private static boolean matchString(String string, String substring, int[] pattern) {
        int i = 0;
        int j = 0;
        while(i+substring.length()-j<=string.length()){
            if(string.charAt(i) == substring.charAt(j)){
                i++;
                j++;
                if(j == substring.length())
                    return true;
            }else{
                if(j>0)
                    j = pattern[j-1] + 1;
                else
                    i++;
            }
        }
        return false;
    }

    private static int[] buildPattern(String substring) {
        int [] pattern = new int[substring.length()];
        Arrays.fill(pattern,-1);
        int j = 0;
        int i = 1;
        while(i<substring.length()){
            if(substring.charAt(i) == substring.charAt(j)){
                pattern[i] = j;
                i++;
                j++;
            }else{
                if(j>0)
                    j = pattern[j-1] + 1;
                else
                    i++;
            }
        }
        return pattern;
    }
}
```
### 

#### - JAVA Solution
```java
```
### 
