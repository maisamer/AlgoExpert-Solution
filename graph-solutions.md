## AlgoExpert Graph Problems

### Depth First Search

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
class Node {
public:
  string name;
  vector<Node *> children;

  Node(string str) { name = str; }

  vector<string> depthFirstSearch(vector<string> *array) {
    Node *node = this;
    array->push_back(node->name);
    for(auto child : node->children)
      child->depthFirstSearch(array);
    return *array;
  }
  Node *addChild(string name) {
    Node *child = new Node(name);
    children.push_back(child);
    return this;
  }
};
```
### Single Cycle Check

#### - CPP Solution
```cpp
using namespace std;

bool hasSingleCycle(vector<int> array) {
  int n = array.size();
  int cnt = n;
  int index = 0;
  while(cnt >= 0){
    if(cnt == 0 and index == 0)
      return true;
    else if((cnt != n and index == 0) or (cnt == 0 and index != 0))
      return false;
    cnt--;
    int step = array[index];
    index = (index + step) % n;
    index = index>=0 ? index : index+n;
  }
  return false;
}
```
### Breadth First Search

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

class Node {
public:
  string name;
  vector<Node *> children;

  Node(string str) { name = str; }

  vector<string> breadthFirstSearch(vector<string> *array) {
    queue<Node *> q;
    q.push(this);
    while(!q.empty()){
      int sz = q.size();
      while(sz--){
        Node *curr = q.front();
        array->push_back(curr->name);
        q.pop();
        for(auto child : curr->children)
          q.push(child);
      }
    }
    return *array;
  }

  Node *addChild(string name) {
    Node *child = new Node(name);
    children.push_back(child);
    return this;
  }
};
```
### River Sizes

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
bool valid(int x,int y,int n,int m){
  return x>=0 and y>=0 and x<n and y<m;
}
int getRiverSize(vector<vector<int>> &matrix,int startX,int startY) {
  if(!valid(startX,startY,matrix.size(),matrix[0].size()) or !matrix[startX][startY])
    return 0;
  matrix[startX][startY] = 0;
  return 1 + getRiverSize(matrix,startX+1,startY)+
  getRiverSize(matrix,startX,startY+1)+
  getRiverSize(matrix,startX-1,startY)+
  getRiverSize(matrix,startX,startY-1);
}
vector<int> riverSizes(vector<vector<int>> matrix) {
  vector<int> ans;
  for(int i=0;i<matrix.size();i++){
    for(int j=0;j<matrix[i].size();j++){
      if(matrix[i][j])
        ans.push_back(getRiverSize(matrix,i,j));
    }
  }
  return ans;
}
```
### Youngest Common Ancestor

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

class AncestralTree {
public:
  char name;
  AncestralTree *ancestor;

  AncestralTree(char name) {
    this->name = name;
    this->ancestor = nullptr;
  }

  void addAsAncestor(vector<AncestralTree *> descendants);
};
int getDepth(AncestralTree *root,AncestralTree *node){
  if(node->name == root->name)
    return 0;
  return 1 + getDepth(root,node->ancestor);
}

AncestralTree *getYoungestCommonAncestor(AncestralTree *topAncestor,
                                         AncestralTree *descendantOne,
                                         AncestralTree *descendantTwo) {
  int d1 = getDepth(topAncestor,descendantOne);
  int d2 = getDepth(topAncestor,descendantTwo);
  if(d1 > d2){
    int steps = d1 - d2;
    while(steps--){
      descendantOne = descendantOne->ancestor;
    }
  }else{
    int steps = d2 - d1;
    while(steps--){
      descendantTwo = descendantTwo->ancestor;
    }
  }
  while(descendantOne->name != descendantTwo->name){
    descendantTwo = descendantTwo->ancestor;
    descendantOne = descendantOne->ancestor;
  }
  return descendantTwo;
}
```
### Youngest Common Ancestor another approach 

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

class AncestralTree {
public:
  char name;
  AncestralTree *ancestor;

  AncestralTree(char name) {
    this->name = name;
    this->ancestor = nullptr;
  }

  void addAsAncestor(vector<AncestralTree *> descendants);
};

AncestralTree *getYoungestCommonAncestor(AncestralTree *node,
                                         AncestralTree *descendantOne,
                                         AncestralTree *descendantTwo) {
  unordered_set<char> visited;
  while(descendantOne){
    visited.insert(descendantOne->name);
    descendantOne = descendantOne->ancestor;
  }
  while(descendantTwo){
    if(visited.find(descendantTwo->name) != visited.end())
      return descendantTwo;
    descendantTwo = descendantTwo->ancestor;
  }
  return nullptr;
}
```
### Remove Islands

#### - CPP Solution
```cpp
#include <vector>
using namespace std;
bool valid(int x,int y,int n,int m){
  return x>=0 and y>=0 and x<n and y<m;
}
void updateArea(vector<vector<int>> &matrix,int x,int y,int value,int n,int m){
  if(!valid(x,y,n,m) or matrix[x][y] != 1)
    return ;
  matrix[x][y] = value;
  updateArea(matrix,x+1,y,value,n,m);
  updateArea(matrix,x,y+1,value,n,m);
  updateArea(matrix,x-1,y,value,n,m);
  updateArea(matrix,x,y-1,value,n,m);
}
vector<vector<int>> removeIslands(vector<vector<int>> matrix) {
  int n = matrix.size();
  int m = matrix[0].size();
  for(int i=0;i<n;i++){
    if(matrix[i][0] == 1)
      updateArea(matrix,i,0,2,n,m);
    if(matrix[i][m-1] == 1)
      updateArea(matrix,i,m-1,2,n,m);
  }
  for(int i=0;i<m;i++){
    if(matrix[0][i] == 1)
      updateArea(matrix,0,i,2,n,m);
    if(matrix[n-1][i] == 1)
      updateArea(matrix,n-1,i,2,n,m);
  }
  for(int i=1;i<n-1;i++)
    for(int j=1;j<m-1;j++)
      if(matrix[i][j] == 1)
        updateArea(matrix,i,j,0,n,m);
        
  for(int i=0;i<n;i++)
    for(int j=0;j<m;j++)
      if(matrix[i][j] == 2)
        matrix[i][j] = 1;
  
  return matrix;
}
```
### cycle In Graph

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public boolean cycleInGraph(int[][] edges) {
        // Write your code here.
        Set<Integer> vis = new HashSet<>();
        Set<Integer> inStack = new HashSet<>();
        for(int i=0;i<edges.length;i++){
            if(!vis.contains(i)){
                if(hasCycle(i,edges,vis,inStack))
                    return true;
            }
        }
        return false;
    }

    private boolean hasCycle(int vertex, int[][] edges, Set<Integer> vis, Set<Integer> inStack) {
        vis.add(vertex);
        inStack.add(vertex);
        for(int i=0;i<edges[vertex].length;i++){
            if(!vis.contains(edges[vertex][i])){
                if(hasCycle(edges[vertex][i],edges,vis,inStack))
                    return true;
            }else{
                if(inStack.contains(edges[vertex][i]))
                    return true;
            }
        }
        inStack.remove(vertex);
        return false;
    }
}
```
### minimum Passes Of Matrix

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public int minimumPassesOfMatrix(int[][] matrix) {
        // Write your code here.
        Queue<List<Integer>> q = new LinkedList<>();
        int[] dx = new int[]{1,-1,0,0};
        int[] dy = new int[]{0,0,1,-1};
        int passes = 0;
        int height = matrix.length;
        int width = matrix[0].length;
        for(int i=0;i<height;i++)
            for(int j=0;j<width;j++)
                if(matrix[i][j] > 0)
                    q.add(List.of(i,j));
        while(!q.isEmpty()){
            int sz = q.size();
            boolean countPass = false;
            while (sz>0){
                List<Integer> point = q.remove();
                for(int i=0;i<4;i++){
                    int x = point.get(0)+dx[i];
                    int y = point.get(1)+dy[i];
                    if(valid(x,y,height,width) && matrix[x][y] < 0) {
                        if(!countPass){
                          passes++;
                          countPass = true;
                        }
                        q.add(List.of(x, y));
                        matrix[x][y] *=-1;
                    }
                }
                sz--;
            }
        }
        for (int[] ints : matrix)
            for (int anInt : ints)
                if (anInt < 0)
                    return -1;
        return passes;
    }

    private boolean valid(int x, int y, int height, int width) {
        return x<height && x>=0 && y<width && y>=0;
    }
}
```
### Two Colorable

#### - JAVA Solution
```java
import java.util.*;

class Program {

    public boolean twoColorable(int[][] edges) {
        // Write your code here.
        int [] colors = new int[edges.length];
        colors[0] = 1;
        if(isTwoColorable(0,edges,colors,1,2))
            return true;
        return false;
    }

    private boolean isTwoColorable(int vertex, int[][] edges, int[] colors, int color, int opposite) {
        for(int sibling : edges[vertex]){
            if(colors[sibling] == 0){
                colors[sibling] = opposite;
                if(!isTwoColorable(sibling,edges,colors,opposite,color))
                    return false;
            } else if (color == colors[sibling]) {
                return false;
            }
        }
        return true;
    }
}
```
### boggle Board

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static List<String> boggleBoard(char[][] board, String[] words) {
        // Write your code here.
        int h = board.length,w=board[0].length;
        Trie trie = new Trie();
        for(String word : words)
            trie.insert(word);
        boolean[][] taken = new boolean[h][w];
        Set<String> searchResultSet = new HashSet<>();
        for(int i=0;i<h;i++){
            for(int j=0;j<w;j++){
                searchForWord(i,j,board,taken, trie.root, searchResultSet);
            }
        }
        return new ArrayList<>(searchResultSet);
    }

    private static void searchForWord(int sx,int sy, char[][] board, boolean[][] taken,
                                      TrieNode root, Set<String> searchResultSet) {
        char currentChar = board[sx][sy];
        if(taken[sx][sy] || !root.children.containsKey(currentChar))
            return;
        taken[sx][sy] = true;
        TrieNode trieNode = root.children.get(currentChar);
        if(trieNode.children.containsKey('*'))
            searchResultSet.add(trieNode.word);
        int[] dx = new int[]{1,-1,0,0,1,-1,1,-1};
        int[] dy = new int[]{0,0,1,-1,1,-1,-1,1};
        int h = board.length,w=board[0].length;
        for(int i=0;i<8;i++){
            int x = sx + dx[i];
            int y = sy + dy[i];
            if(valid(x,y,h,w)&&!taken[x][y]){
                searchForWord(x,y,board,taken,trieNode,searchResultSet);
            }
        }
        taken[sx][sy] = false;
    }

    private static boolean valid(int x,int y,int h,int w){
        return x>=0&&x<h&&y>=0&&y<w;
    }

    public static class TrieNode{
        Map<Character,TrieNode> children = new HashMap<>();
        String word;
    }

    public static class Trie{
        TrieNode root = new TrieNode();
        char endSymbol = '*';
        void insert(String word){
            TrieNode curr = root;
            for(int i=0;i<word.length();i++){
                char c = word.charAt(i);
                if(!curr.children.containsKey(c))
                    curr.children.put(c,new TrieNode());
                curr = curr.children.get(c);
            }
            curr.children.put(endSymbol,null);
            curr.word = word;
        }

    }
}
```
### Largest Island

#### - JAVA Solution
```java
import java.util.*;

class Program {
    // O(w^2 * h^2) time | O(w * h) space
    public int largestIsland(int[][] matrix) {
        // Write your code here.
        int mxLen = 0;
        for(int i=0;i< matrix.length;i++){
            for(int j=0;j<matrix[0].length;j++){
                boolean[][] vis = new boolean[matrix.length][matrix[0].length];
                if(matrix[i][j] > 0){
                    matrix[i][j] = 0;
                    mxLen = Math.max(dfs(i,j,matrix,vis),mxLen);
                    matrix[i][j] = 1;
                }
            }
        }
        return mxLen == 0 ? matrix.length*matrix[0].length :mxLen;
    }

    private int dfs(int x, int y, int[][] matrix,boolean[][] vis) {
        vis[x][y] = true;
        int [] dx = {1,-1,0,0};
        int [] dy = {0,0,1,-1};
        int cnt = 1;
        for(int i=0;i<4;i++){
            int newX = x+dx[i];
            int newY = y+dy[i];
            if(valid(newX,newY, matrix.length ,matrix[0].length) && !vis[newX][newY]
                    && matrix[newX][newY] == 0){
                cnt+= dfs(newX,newY,matrix,vis);
            }
        }
        return cnt;
    }
    private boolean valid(int x, int y, int height, int width) {
        return x<height && x>=0 && y<width && y>=0;
    }
}
```

#### - another Solution
```java
import java.util.*;

class Program {
    final int [] dx = {1,-1,0,0};
    final int [] dy = {0,0,1,-1};
    // O(w * h) time | O(w * h) space
    public int largestIsland(int[][] matrix) {
        int mxSize = 0;
        // Write your code here.
        ArrayList<Integer> islandSizes = new ArrayList<>();
        int islandId = 2;
        for(int i=0;i<matrix.length;i++){
            for(int j=0;j<matrix[0].length;j++){
                if(matrix[i][j] == 0) {
                    islandSizes.add(getIslandSize(i, j, matrix, islandId));
                    islandId++;
                }
            }
        }
        for(int i=0;i<matrix.length;i++){
            for(int j=0;j<matrix[0].length;j++){
                if(matrix[i][j] == 1) {
                    Set<Integer> adjIslands = new HashSet<>();
                    int connectedIslandsSize = 0;
                    for(int adj=0;adj<4;adj++){
                        int newX = i+dx[adj];
                        int newY = j+dy[adj];
                        if(valid(newX,newY, matrix.length ,matrix[0].length) && matrix[newX][newY] != 1){
                            if(adjIslands.contains( matrix[newX][newY]))
                                continue;
                            adjIslands.add(matrix[newX][newY]);
                            connectedIslandsSize+=islandSizes.get(matrix[newX][newY]-2);
                        }
                    }
                    mxSize = Math.max(connectedIslandsSize+1,mxSize);
                }
            }
        }
        return mxSize;
    }

    private Integer getIslandSize(int row, int col, int[][] matrix, int islandId) {
        matrix[row][col] = islandId;
        int cnt = 1;
        for(int i=0;i<4;i++){
            int newX = row+dx[i];
            int newY = col+dy[i];
            if(valid(newX,newY, matrix.length ,matrix[0].length) && matrix[newX][newY] == 0){
                cnt+= getIslandSize(newX,newY,matrix,islandId);
            }
        }
        return cnt;
    }

    private boolean valid(int x, int y, int height, int width) {
        return x<height && x>=0 && y<width && y>=0;
    }
}
```
### rectangle Mania

#### - JAVA Solution
```java
import java.util.*;

class Program {
    final static String UP = "UP";
    final static String LEFT = "LEFT";
    final static String RIGHT = "RIGHT";
    final static String DOWN = "DOWN";
    // O(n^2) time | O(n^2) space
    public static int rectangleMania(List<Integer[]> coords) {
        // Write your code here.
        Map<String,Map<String,List<Point>>> coordTable = getCoordTable(coords);
        return getRectangleCount(coords,coordTable);
    }

    private static int getRectangleCount(List<Integer[]> coords, Map<String, Map<String, List<Point>>> coordTable) {
        int rectangleCont = 0;
        for(Integer [] coord:coords){
            rectangleCont += clockWiseCountRectangle(new Point(coord[0],coord[1]),coordTable,UP,new Point(coord[0],coord[1]));
        }
        return rectangleCont;
    }

    private static int clockWiseCountRectangle(Point coord, Map<String, Map<String, List<Point>>> coordTable,
                                               String direction, Point origin) {
        String coordString = PointToString(coord);
        if(direction == LEFT){
            for(Point p : coordTable.get(coordString).get(LEFT)) 
                if(p.x == origin.x && p.y == origin.y)
                    return 1;
            return 0;
        }else{
            int rectangleCont = 0;
            String nextDirection = getNextDirection(direction);
            for(Point p : coordTable.get(coordString).get(direction))
                rectangleCont+=clockWiseCountRectangle(p,coordTable,nextDirection,origin);
            return rectangleCont;
        }
    }

    private static String getNextDirection(String direction) {
        switch (direction){
            case UP -> {
                return RIGHT;
            }
            case RIGHT -> {
                return DOWN;
            }
            case DOWN -> {
                return LEFT;
            }
            default -> {
                return "";
            }
        }
    }

    private static Map<String, Map<String, List<Point>>> getCoordTable(List<Integer[]> coords) {
        Map<String, Map<String, List<Point>>> coordTable = new HashMap<>();
        for(Integer [] coord1 : coords){
            Point x = new Point(coord1[0],coord1[1]);
            Map<String, List<Point>> coordDirections = new HashMap<>();
            coordDirections.put(UP,new ArrayList<>());
            coordDirections.put(DOWN,new ArrayList<>());
            coordDirections.put(RIGHT,new ArrayList<>());
            coordDirections.put(LEFT,new ArrayList<>());
            for(Integer [] coord2:coords){
                Point y = new Point(coord2[0],coord2[1]);
                String direction = getPointDirection(x,y);
                if(coordDirections.containsKey(direction)){
                    coordDirections.get(direction).add(y);
                }
            }
            coordTable.put(PointToString(x),coordDirections);
        }
        return coordTable;
    }

    private static String PointToString(Point x) {
        return Integer.toString(x.x) + '-' + Integer.toString(x.y);
    }

    private static String getPointDirection(Point p1, Point p2) {
        if(p1.x == p2.x) {
            if (p1.y > p2.y)
                return DOWN;
            else if (p1.y < p2.y)
                return UP;
        } else if(p1.y == p2.y) {
            if (p1.x > p2.x)
                return LEFT;
            else if (p1.x < p2.x)
                return RIGHT;
        }
        return "";
    }

    static class Point {
        public int x;
        public int y;

        public Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }
}
```

#### - another Solution
```java
import java.util.*;

class Program {
    public static int rectangleMania(List<Integer[]> coords) {
        // Write your code here.
        int rectangleCount = 0;
        Set<String> points = new HashSet<>();
        for(int i=0;i<coords.size();i++){
            points.add(String.valueOf(coords.get(i)[0]) +'-'+ String.valueOf(coords.get(i)[1]));
        }
        for(int i=0;i<coords.size();i++){
            for(int j=0;j<coords.size();j++){
                if(i == j)
                    continue;
                Point p1 = new Point(coords.get(i)[0],coords.get(i)[1]);
                Point p2 = new Point(coords.get(j)[0],coords.get(j)[1]);
                if(p1.x < p2.x && p1.y < p2.y){
                    String upLeft = String.valueOf(p1.x)+'-'+String.valueOf(p2.y);
                    String bottomRight = String.valueOf(p2.x)+'-'+String.valueOf(p1.y);
                    if(points.contains(upLeft) && points.contains(bottomRight))
                        rectangleCount++;
                        
                }
            }
        }
        return rectangleCount;
    }

    static class Point {
        public int x;
        public int y;

        public Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }
}
```
### Detect Arbitrage (Bellman Ford Algorithm)

#### - JAVA Solution
```java
import java.util.*;

class Program {

    public boolean detectArbitrage(ArrayList<ArrayList<Double>> exchangeRates) {
        ArrayList<ArrayList<Double>> logExchangeRates = getLogExchangeRates(exchangeRates);
        return foundNegativeWeightCycle(logExchangeRates,0);
    }

    private boolean foundNegativeWeightCycle(ArrayList<ArrayList<Double>> graph, int start) {
        double[] distanceFromStart = new double[graph.size()];
        Arrays.fill(distanceFromStart,Double.MAX_VALUE);
        distanceFromStart[start] = 0L;
        for(int i=0;i<graph.size()-1;i++)
            if(!relaxAndUpdateDistance(graph,distanceFromStart))
                return false;
        return relaxAndUpdateDistance(graph,distanceFromStart);
    }

    private boolean relaxAndUpdateDistance(ArrayList<ArrayList<Double>> graph, double[] distanceFromStart) {
        boolean update = false;
        for(int source = 0;source<graph.size();source++){
            for(int destination=0;destination<graph.get(source).size();destination++){
                double edgeWight = graph.get(source).get(destination);
                double newDistanceToDestination = distanceFromStart[source] + edgeWight;
                if(newDistanceToDestination < distanceFromStart[destination]){
                    update = true;
                    distanceFromStart[destination] = newDistanceToDestination;
                }
            }
        }
        return update;
    }

    private ArrayList<ArrayList<Double>> getLogExchangeRates(ArrayList<ArrayList<Double>> exchangeRates) {
        ArrayList<ArrayList<Double>> newGraph = new ArrayList<>();
        for(int i =0;i<exchangeRates.size();i++){
            newGraph.add(new ArrayList<>());
            for (Double rate:exchangeRates.get(i)){
                newGraph.get(i).add(-Math.log10(rate));
            }
        }
        return newGraph;
    }
}
```
### Two-Edge Connected Graph

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public boolean twoEdgeConnectedGraph(int[][] edges) {
        // Write your code here.
        if(edges.length == 0)
            return true;
        int [] arrivalTimes = new int[edges.length];
        Arrays.fill(arrivalTimes,-1);
        if(getMinArrivalTimeFromAncestor(edges,arrivalTimes,0,-1,0) == -1)
            return false;
        return checkConnectedGraph(arrivalTimes);
    }

    private boolean checkConnectedGraph(int[] arrivalTimes) {
        for(int val:arrivalTimes)
            if(val == -1)
                return false;
        return true;
    }

    private int getMinArrivalTimeFromAncestor(int[][] edges, int[] arrivalTimes, int currentVertex, int parent, int currentTime) {
        arrivalTimes[currentVertex] = currentTime;
        int minArrivalTime = currentTime;
        for(int destination : edges[currentVertex]){
            if(arrivalTimes[destination] == -1)
                minArrivalTime = Math.min(minArrivalTime,
                getMinArrivalTimeFromAncestor(edges,arrivalTimes,destination,currentVertex,currentTime+1));
            else if(destination != parent)
                minArrivalTime = Math.min(minArrivalTime,arrivalTimes[destination]);
        }
        if(currentTime == minArrivalTime && parent != -1)
            return -1;
        return minArrivalTime;
    }
}
```
### 

#### - JAVA Solution
```java
```
