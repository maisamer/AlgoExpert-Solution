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
### A* Algorithm

#### - JAVA Solution
```java
import java.util.*;

// Do not edit the class below except for the buildHeap,
// siftDown, siftUp, peek, remove, and insert methods.
// Feel free to add new properties and methods to the class.
class Program {
    public int[][] aStarAlgorithm(
            int startRow, int startCol, int endRow, int endCol, int[][] graph
    ) {
        // Write your code here.
        List<List<Node>> nodes = initialize(graph);
        Node startNode = nodes.get(startRow).get(startCol);
        Node endNode = nodes.get(endRow).get(endCol);
        startNode.distanceFromStart = 0;
        startNode.estimatedDistanceToEnd = calculateManhattanDistance(startNode,endNode);
        List<Node> nodeToVisit = new ArrayList<>();
        nodeToVisit.add(startNode);
        MinHeap minHeap = new MinHeap(nodeToVisit);
        while(!minHeap.isEmpty()){
            Node current = minHeap.remove();
            if(current == endNode)
                break;
            List<Node> neighbours = getNeighbouringNodes(current,nodes);
            for(Node neighbour:neighbours){
                int distance = current.distanceFromStart + 1;
                if(distance >= neighbour.distanceFromStart)
                    continue;
                neighbour.cameFrom = current;
                neighbour.distanceFromStart = distance;
                neighbour.estimatedDistanceToEnd = distance +
                        calculateManhattanDistance(neighbour,endNode);
                if(minHeap.contain(neighbour)){
                    minHeap.update(neighbour);
                }else{
                    minHeap.insert(neighbour);
                }
            }

        }
        return reconstructPath(endNode);
    }

    private int[][] reconstructPath(Node endNode) {
        if(endNode.cameFrom == null)
            return new int[][]{};
        List<List<Integer>> pathList = new ArrayList<>();
        Node current = endNode;
        while(current != null){
            pathList.add(List.of(current.row,current.col));
            current = current.cameFrom;
        }

        int [][] path = new int[pathList.size()][2];
        for(int i=0;i<pathList.size();i++){
            path[i][0] = pathList.get(pathList.size()-1-i).get(0);
            path[i][1] = pathList.get(pathList.size()-1-i).get(1);
        }
        return path;
    }

    private List<Node> getNeighbouringNodes(Node current, List<List<Node>> nodes) {
        List<Node> neighbours = new ArrayList<>();
        int numRows = nodes.size();
        int numCols = nodes.get(0).size();
        int row = current.row;
        int col = current.col;
        if(row+1 < numRows && nodes.get(row+1).get(col).value == 0)
            neighbours.add(nodes.get(row+1).get(col));
        if(row-1 >= 0 && nodes.get(row-1).get(col).value == 0)
            neighbours.add(nodes.get(row-1).get(col));
        if(col+1 < numCols && nodes.get(row).get(col+1).value == 0)
            neighbours.add(nodes.get(row).get(col+1));
        if(col-1 >= 0 && nodes.get(row).get(col-1).value == 0)
            neighbours.add(nodes.get(row).get(col-1));
        return neighbours;
    }

    private List<List<Node>> initialize(int[][] graph) {
        List<List<Node>> nodes = new ArrayList<>();
        for(int i=0;i<graph.length;i++){
            List<Node> nodeList = new ArrayList<>();
            nodes.add(nodeList);
            for(int j=0;j<graph[i].length;j++){
                nodes.get(i).add(new Node(i,j,graph[i][j]));
            }
        }
        return nodes;
    }

    int calculateManhattanDistance(Node start,Node end){
        return Math.abs(start.row - end.row) + Math.abs(start.col - end.col);
    }

    class Node{
        String id;
        int row;
        int col;
        int value;
        Node cameFrom;
        int distanceFromStart;
        int estimatedDistanceToEnd;
        public Node(int row, int col, int value) {
            this.id = String.valueOf(row) + '-' + String.valueOf(col);
            this.row = row;
            this.col = col;
            this.value = value;
            this.cameFrom = null;
            this.distanceFromStart = Integer.MAX_VALUE;
            this.estimatedDistanceToEnd = Integer.MAX_VALUE;
        }
    }

    class MinHeap {
        List<Node> heap = new ArrayList<>();
        Map<String,Integer> nodePositionInHeap = new HashMap<>();
        public MinHeap(List<Node> array) {
            for(int i=0;i<array.size();i++)
                nodePositionInHeap.put(array.get(i).id,i);
            heap = buildHeap(array);
        }

        public List<Node> buildHeap(List<Node> array) {
            // Write your code here.
            int firstParentIdx = (array.size() - 2)/2;
            for(int currentIdx = firstParentIdx;currentIdx>=0;currentIdx--)
                siftDown(currentIdx,array.size()-1,array);
            return array;
        }

        public void siftDown(int currentIdx, int endIdx, List<Node> heap) {
            // Write your code here.
            int childOneIdx = currentIdx*2 + 1;
            while(childOneIdx <= endIdx){
                int childTwoIdx = childOneIdx + 1;
                if(childTwoIdx > endIdx)
                    childTwoIdx = -1;
                if(childTwoIdx != -1 && heap.get(childTwoIdx).estimatedDistanceToEnd <
                        heap.get(childOneIdx).estimatedDistanceToEnd)
                    childOneIdx = childTwoIdx;
                if(heap.get(childOneIdx).estimatedDistanceToEnd <
                        heap.get(currentIdx).estimatedDistanceToEnd){
                    swap(childOneIdx,currentIdx);
                    currentIdx = childOneIdx;
                    childOneIdx = currentIdx*2 + 1;
                }else
                    break;
            }
        }

        private void swap(int i, int j) {
            nodePositionInHeap.put(heap.get(i).id,j);
            nodePositionInHeap.put(heap.get(j).id,i);
            Node temp = heap.get(i);
            heap.set(i,heap.get(j));
            heap.set(j,temp);
        }

        void siftUp(int currentIdx) {
            int parentIdx = (currentIdx - 1)/2;
            while(currentIdx > 0 && heap.get(currentIdx).estimatedDistanceToEnd <
                    heap.get(parentIdx).estimatedDistanceToEnd){
                swap(currentIdx,parentIdx);
                currentIdx = parentIdx;
                parentIdx = (currentIdx - 1)/2;
            }
        }

        Node peek() {
            return heap.isEmpty() ? null : heap.get(0);
        }

        Node remove() {
            if(heap.isEmpty())
                return null;
            Node removedElement = heap.get(0);
            swap(0,heap.size()-1);
            heap.remove(heap.size()-1);
            nodePositionInHeap.remove(removedElement.id);
            siftDown(0,heap.size()-1,heap);
            return removedElement;
        }

        void insert(Node value) {
            heap.add(value);
            nodePositionInHeap.put(value.id,heap.size()-1);
            siftUp(heap.size()-1);
        }

        boolean contain(Node node){
            return nodePositionInHeap.containsKey(node.id);
        }

        void update(Node node){
            siftUp(nodePositionInHeap.get(node.id));
        }

        public boolean isEmpty() {
            return heap.isEmpty();
        }
    }
}
```
### prims Algorithm

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public int[][][] primsAlgorithm(int[][][] edges) {
        // Write your code here.
        List<List<int[]>> mstList = new ArrayList<>();
        int[][][] mst = new int[edges.length][][];
        PriorityQueue<Item> minHeap = new PriorityQueue<>();
        for(int[] edge:edges[0])
            minHeap.add(new Item(0,edge[0],edge[1]));
        for(int i=0;i<edges.length;i++)
            mstList.add(new ArrayList<>());
        while (!minHeap.isEmpty()){
            Item item = minHeap.remove();
            if(mstList.get(item.destination).isEmpty()) {
                mstList.get(item.vertex).add(new int[]{item.destination, item.weight});
                mstList.get(item.destination).add(new int[]{item.vertex, item.weight});
                for (int[] edge : edges[item.destination])
                    if (mstList.get(edge[0]).isEmpty())
                        minHeap.add(new Item(item.destination, edge[0], edge[1]));
            }
        }
        for(int i=0;i< mstList.size();i++){
            mst[i] = new int[mstList.get(i).size()][];
            for(int j=0;j<mstList.get(i).size();j++)
                mst[i][j] = mstList.get(i).get(j);
        }
        return mst;
    }
    class Item implements Comparable<Item>{
        int vertex;
        int destination;
        int weight;

        public Item(int vertex, int destination, int weight) {
            this.vertex = vertex;
            this.destination = destination;
            this.weight = weight;
        }
        @Override
        public int compareTo(Item other) {
            // Compare items based on their weight
            return Integer.compare(this.weight, other.weight);
        }
    }
}
```
