### longest Balanced Substring

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public int longestBalancedSubstring(String string) {
        // Write your code here.
        int mxSz = 0;
        int opening = 0,closing=0;
        for(int i = 0; i<string.length(); i++){
            if(string.charAt(i) == '(')
                opening++;
            else 
                closing++;
            if(opening == closing)
                mxSz = Math.max(mxSz,opening+closing);
            else if(closing > opening){
                closing = 0;
                opening = 0;
            }
        }
        opening = 0;
        closing=0;
        for(int i = string.length()-1; i>=0; i--){
            if(string.charAt(i) == '(')
                opening++;
            else
                closing++;
            if(opening == closing)
                mxSz = Math.max(mxSz,opening+closing);
            else if(closing < opening){
                closing = 0;
                opening = 0;
            }
        }
        return mxSz;
    }

}
```
#### - another solution using stack
```java
import java.util.*;

class Program {
    public int longestBalancedSubstring(String string) {
        // Write your code here.
        int mxSz = 0;
        Stack<Integer> stack = new Stack<>();
        stack.push(-1);
        for(int i = 0; i<string.length(); i++){
            if(string.charAt(i) == '(')
                stack.push(i);
            else {
                stack.pop();
                if(stack.empty())
                    stack.push(i);
                else{
                    int start = stack.peek();
                    mxSz = Math.max(mxSz,i - start);
                }
            }
        }
        return mxSz;
    }

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
### 
