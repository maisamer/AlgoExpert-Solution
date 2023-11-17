## Stacks Problems

### Min Max Stack Construction

#### - JAVA Solution
```java
import java.util.*;

class Program {
    // Feel free to add new properties and methods to the class.
    static class MinMaxStack {
        List<Integer> s = new ArrayList<>();
        List<List<Integer>> minMaxStack = new ArrayList<>();
        public int peek() {
            // Write your code here.
            if(s.size() > 0)
                return s.get(s.size()-1);
            return -1;
        }

        public int pop() {
            // Write your code here.
            int item = -1;
            if(s.size() > 0) {
                item = s.get(s.size()-1);
                s.remove(s.size()-1);
                minMaxStack.remove(minMaxStack.size()-1);
            }
            return item;
        }

        public void push(Integer number) {
            // Write your code here.
            s.add(number);
            int mn = number,mx = number;
            if(minMaxStack.size() > 0){
                if(number > minMaxStack.get(minMaxStack.size()-1).get(0))
                    mn = minMaxStack.get(minMaxStack.size()-1).get(0);
                if(number < minMaxStack.get(minMaxStack.size()-1).get(1))
                    mx = minMaxStack.get(minMaxStack.size()-1).get(1);
            }
            minMaxStack.add(new ArrayList<>(List.of(mn,mx)));
        }

        public int getMin() {
            // Write your code here.
            return minMaxStack.get(minMaxStack.size()-1).get(0);
        }

        public int getMax() {
            // Write your code here.
            return minMaxStack.get(minMaxStack.size()-1).get(1);
        }
    }
}
```
### Balanced Brackets
#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static boolean balancedBrackets(String str) {
        // Write your code here.
        Stack<Character> s = new Stack<>();
        for(int i=0;i<str.length();i++){
            if(List.of('(','[','{').contains(str.charAt(i))){
                s.push(str.charAt(i));
            }else if(List.of(')',']','}').contains(str.charAt(i))){
              if(s.empty())
                return false;
                Character c = s.pop();
                if((str.charAt(i) == ')' && c != '(') || (str.charAt(i) == ']' && c != '[') || (str.charAt(i) == '}' && c != '{'))
                    return false;
            }
        }
        return s.empty();
    }
}
```
### Sunset Views

#### - JAVA Solution
```java
import java.util.*;

class Program {

    public ArrayList<Integer> sunsetViews(int[] buildings, String direction) {
        // Write your code here.
        ArrayList<Integer> res = new ArrayList<>();
        boolean backward = direction.equals("EAST");
        int i = backward?buildings.length-1:0;
        int step = backward?-1:1;
        int mn = 0;
        while(i>=0 && i < buildings.length){
            if(buildings[i]>mn){
                mn = buildings[i];
                if(backward)
                    res.add(0,i);
                else
                    res.add(i);
            }
            i+=step;
        }
        return res;
    }
}
```
### Best Digits

#### - JAVA Solution
```java
import java.util.Stack;

class Program {
    public String bestDigits(String number, int numDigits) {
        // Write your code here.
        Stack<Character> s = new Stack<>();
        StringBuffer ans = new StringBuffer();
        for(int i=0;i<number.length();i++){
            while(!s.empty() && s.peek()<number.charAt(i) && numDigits > 0){
              numDigits--;
              s.pop();
            }
            s.push(number.charAt(i));
        }
        while(numDigits > 0){
            numDigits--;
            s.pop();
        }
        while(!s.empty()){
            ans.append(s.pop());
        }
        return ans.reverse().toString();
    }
}
```
### Sort Stack

#### - JAVA Solution
```java
import java.util.*;

class Program {

    public ArrayList<Integer> sortStack(ArrayList<Integer> stack) {
        // Write your code here.
        if(stack.size() == 0)
            return stack;
        int top = stack.get(stack.size() - 1);
        stack.remove(stack.size()-1);
        sortStack(stack);
        insertTopToCorrectPlace(stack,top);
        return stack;
    }

    private void insertTopToCorrectPlace(ArrayList<Integer> stack, int top) {
        if(stack.size() == 0 || top > stack.get(stack.size() - 1)) {
            stack.add(top);
        }else{
            int removedTop = stack.get(stack.size()-1);
            stack.remove(stack.size()-1);
            insertTopToCorrectPlace(stack,top);
            stack.add(removedTop);
        }
    }
}
```
### Next Greater Element

#### - JAVA Solution
```java
import java.util.*;

class Program {

    public int[] nextGreaterElement(int[] array) {
        // Write your code here.
        Stack<Integer> s = new Stack<>();
        int[] ans = new int[array.length];
        Arrays.fill(ans,-1);
        for(int it=0;it<2*array.length;it++){
            int i = it%array.length;
            while(!s.empty() && array[s.peek()] < array[i]){
                ans[s.peek()] = array[i];
                s.pop();
            }
            s.push(i);
        }
        return ans;
    }
}
```
### Reverse Polish Notation

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public int reversePolishNotation(String[] tokens) {
    // Write your code here.
    Stack<Integer> s = new Stack<>();
    int ans = 0;
    for(String tocken:tokens){
      if(tocken.length() == 1 && isOperation(tocken)){
        int second = s.pop();
        int first = s.pop();
        int opResult = getResult(first,second,tocken.charAt(0));
        s.push(opResult);
      }else{
        s.push(Integer.parseInt(tocken));
      }
    }
    while(!s.empty()){
      ans+=s.pop();
    }
    return ans;
  }
  private int getResult(int first,int second,char op){
    if(op == '+')
      return first+second;
    if(op == '-')
      return first-second;
    if(op == '*')
      return first*second;
    return first/second;
  }
  private boolean isOperation(String tocken){
    return tocken.charAt(0) == '+' || tocken.charAt(0) == '-' || 
      tocken.charAt(0) == '*' || tocken.charAt(0) == '/';
  }
  
}
```
### Colliding Asteroids

#### - JAVA Solution
```java
import java.lang.reflect.Array;
import java.util.*;

class Program {
    public int[] collidingAsteroids(int[] asteroids) {
        // Write your code here.
        Stack<Integer> s = new Stack<>();
        for(int asteroid:asteroids){
            if(asteroid > 0 || s.empty() || s.peek()<0)
                s.push(asteroid);
            while(!s.empty() && s.peek()*asteroid < 0){
                if(s.peek() == Math.abs(asteroid)) {
                    s.pop();
                    break;
                }
                if(s.peek() > Math.abs(asteroid)) {
                    break;
                }
                s.pop();
                if(s.empty() || s.peek() < 0)
                    s.push(asteroid);
            }
        }
        int [] ans = new int[s.size()];
        for(int i=ans.length-1;i>=0;i--)
            ans[i] = s.pop();
        return ans;
    }
}
```
### Shorten Path

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static String shortenPath(String path) {
        // Write your code here;
        Stack<String> s = new Stack<>();
        boolean isRoot = path.charAt(0) == '/';
        String[] tokens = path.split("/");
        List<String> tokenList = Arrays.asList(tokens);
        List<String> filteredToken = tokenList.stream().filter(token -> token.length()>0 && !token.equals("."))
                .toList();
        if(isRoot) s.push("");
        for(String token:filteredToken){
            if(token.equals("..")){
                if(s.empty() || s.peek().equals(".."))
                    s.push(token);
                else if(!s.peek().equals(""))
                    s.pop();
            }else{
                s.push(token);
            }
        }
        if(s.size() == 1 && s.peek().equals("")) return "/";
        return String.join("/",s);
    }
}
```
### largest Rectangle Under Skyline

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public int largestRectangleUnderSkyline(ArrayList<Integer> buildings) {
    // Write your code here.
    int maxArea = 0;
    for(int i=0;i<buildings.size();i++){
      int left = i;
      while(left>0 && buildings.get(left-1)>=buildings.get(i))
        left--;
      int right = i;
      while(right<buildings.size()-1 && buildings.get(right+1)>=buildings.get(i))
        right++;
      maxArea = Math.max(maxArea,buildings.get(i) * (right-left+1));
    }
    return maxArea;
  }
}
```
### Largest Park

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public int largestPark(boolean[][] land) {
        // Write your code here.
        int h = land.length,w=land[0].length;
        int []heights = new int[w];
        int maxArea = 0;
        for(int row=0;row<h;row++){
            for(int col=0;col<w;col++)
                heights[col] = land[row][col] ? 0 : heights[col]+1;
            maxArea = Math.max(maxArea,largestRectangleHistogram(heights));
        }
        return maxArea;
    }

    private int largestRectangleHistogram(int[] heights) {
        int maxArea = 0;
        Stack<Integer> stack = new Stack<>();
        for(int i=0;i<heights.length;i++){
            while(!stack.empty() && heights[stack.peek()]>heights[i]){
                int h = heights[stack.pop()];
                int w = stack.empty() ? i:i-stack.peek()-1;
                maxArea=Math.max(h*w,maxArea);
            }
            stack.push(i);
        }
        while (!stack.empty()){
            int h = heights[stack.pop()];
            int w = stack.empty() ? heights.length:heights.length-stack.peek()-1;
            maxArea=Math.max(h*w,maxArea);
        }
        return maxArea;
    }
}
```
