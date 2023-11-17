## String Problems

### Palindrome Check

#### - CPP Solution
```cpp
using namespace std;

bool isPalindrome(string str) {
  int l=0,r=str.size()-1;
  while(l<r)
    if(str[l++] != str[r--])
      return false;
  return true;
}
```
### Caesar Cypher Encryptor

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public static String caesarCypherEncryptor(String str, int key) {
    String res = "";
    key = key % 26;
    for (int i = 0; i < str.length(); i++){
      int ascii = str.charAt(i);
      if(ascii + key > 122){
        ascii = (key - (122 - ascii) ) + 96;
      }else{
        ascii += key;
      }
      char asciiToChar = (char) ascii;
      res += asciiToChar;
    }
    return res;
  }
}
```
### Run-Length Encoding

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public String runLengthEncoding(String string) {
    StringBuilder res = new StringBuilder();
    for(int i=0;i<string.length();i++){
      char c = string.charAt(i);
      int cnt = 1;
      while(i+1 < string.length() && string.charAt(i) == string.charAt(i+1) && cnt < 9){
        cnt++;
        i++;
      }
      res.append(cnt+"");
      res.append(c);
    }
    return res.toString();
  }
}
```
### Common Characters

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static String[] commonCharacters(String[] strings) {
        // Write your code here.
        Map<Character,Set<Integer>> dic = new HashMap<>();
        int k=0;
        for(String str:strings){
            k++;
            for(int i=0;i<str.length();i++){
                if(dic.containsKey(str.charAt(i))){
                    dic.get(str.charAt(i)).add(k);
                }else{
                    Set s = new HashSet<>();
                    s.add(k);
                    dic.put(str.charAt(i),s);
                }
            }
        }
        List<String> res = new ArrayList<String>();
        for(var e:dic.entrySet()){
            if(e.getValue().size() == strings.length){
                res.add(""+e.getKey());
            }
        }

        return res.stream().toArray(String[] ::new);
    }
}
```
### Generate Document

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public boolean generateDocument(String characters, String document) {
        // Write your code here.
        Map<Character,Integer> freqMap = new HashMap<>();
        for(int i=0;i < characters.length();i++){
            Character c = characters.charAt(i);
            if(!freqMap.containsKey(c)){
                freqMap.put(c,1);
            }else{
                freqMap.put(c,freqMap.get(c) + 1);
            }
        }
        for(int i=0;i<document.length();i++){
            Character c = document.charAt(i);
            if(freqMap.containsKey(c) && freqMap.get(c) > 0)
                freqMap.put(c,freqMap.get(c) -1);
            else 
                return false;
        }
        return true;
    }
}
```
### First Non-Repeating Character

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public int firstNonRepeatingCharacter(String s) {
        Map<Character,Integer[]> m = new HashMap<>();
        for(int i=0;i<s.length();i++){
            Character c = s.charAt(i);
            if(m.containsKey(c)){
                m.get(c)[0]++;
            }else{
                m.put(c,new Integer[]{1,i});
            }
        }
        int ind = -1;
        for(Integer[] item : m.values()){
            if(item[0] == 1 && (ind == -1 || item[1]<ind)){
                ind = item[1];
            }
        }
        return ind;
    }
}
```
### Semordnilap

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public ArrayList<ArrayList<String>> semordnilap(String[] words) {
        // Write your code here.
        HashSet<String> m = new HashSet<>(List.of(words));
        ArrayList<ArrayList<String>> ans = new ArrayList<>();
        for(int i=0;i< words.length;i++){
            String reversed = new StringBuilder((words[i])).reverse().toString();
            if(m.contains(reversed) && !reversed.equals(words[i])){
                ArrayList<String> pair = new ArrayList<>();
                pair.add(words[i]);
                pair.add(reversed);
                ans.add(pair);
                m.remove(words[i]);
                m.remove(reversed);
            }
        }
        return ans;
    }
}
```
### Longest Palindromic Substring

#### - CPP Solution
```cpp
using namespace std;
string getLongestPalindromic(string s,int sz){
  string res = "";
  for(int i=0;i<s.size();i++){
    int l = i;
    int r = i+sz;
    while(l>=0 && r<s.size() && s[l] == s[r]){
      if(res.size() < r-l+1){
        res = s.substr(l,r-l+1);
      }
      l--;
      r++;
    }
  }
  return res;
}
string longestPalindromicSubstring(string s) {
  if(s.empty())
    return s;
  string s1 = getLongestPalindromic(s,0);
  string s2 = getLongestPalindromic(s,1);
  return s1.size() > s2.size() ? s1:s2;
}
```
### Group Anagrams

#### - CPP Solution
```cpp
#include <vector>

using namespace std;

vector<vector<string>> groupAnagrams(vector<string> words) {
  // Write your code here.
  vector<vector<string>> ans;
  unordered_map<string,vector<string>> m;
  for(int i=0;i<words.size();i++){
    string sorted = words[i];
    sort(sorted.begin(),sorted.end());
    m[sorted].push_back(words[i]);
  }
  for(auto [key,value]:m)
    ans.push_back(value);
  return ans;
}
```
### Valid IP Addresses

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public boolean valid(String part){
    return part.length() == 1 || Integer.parseInt(part) < 256 &&(part.length() > 1 && part.charAt(0) != '0');
  }
  public void backtrack(ArrayList<String> ans,String s,int i,int dots,String ip,String rem){
    if(i >= s.length()){
      if(dots == 0)
        ans.add(ip);
      return;
    }
    if(rem.length() + 1 <= 3 && valid(rem+s.charAt(i)))
      backtrack(ans,s,i+1,dots,ip+s.charAt(i),rem + s.charAt(i));
    String dummy = rem + s.charAt(i);
    if(dots>0 && i < s.length() -1 && valid(dummy))
      backtrack(ans,s,i+1,dots-1,ip+s.charAt(i)+".","");
  }
  public ArrayList<String> validIPAddresses(String string) {
    ArrayList<String> ans = new ArrayList<String>();
    if(string.charAt(0) != '0')
      backtrack(ans,string,0,3,"","");
    return ans;
  }
}
```

### another approach

#### - JAVA Solution
```java
import java.util.*;

class Program {
  public boolean valid(String part){
    return part.length() == 1 || Integer.parseInt(part) < 256 &&(part.length() > 1 && part.charAt(0) != '0');
  }
  public ArrayList<String> validIPAddresses(String string) {
    ArrayList<String> ans = new ArrayList<String>();
    for(int i=0;i<string.length()-3;i++){
      String p1 = string.substring(0,i+1);
      if(!valid(p1))
        break;
      for(int k=i+1;k<string.length()-2;k++){
        String p2 = string.substring(i+1,k+1);
        if(!valid(p2))
          break;
        for(int m=k+1;m<string.length()-1;m++){
          String p3 = string.substring(k+1,m+1);
          if(!valid(p3))
            break;
          String p4 = string.substring(m+1,string.length());
          if(valid(p4))
            ans.add(p1+"."+p2+"."+p3+"."+p4);
        }
      }
    }
    return ans;
  }
}
```
### Reverse Words In String

#### - CPP Solution
```cpp
using namespace std;

string reverseWordsInString(string str) {
  // Write your code here.
  string ans;
  int counter=0,start=-1;
  for(int i = str.size()-1;i>=0;i--){
    if(str[i] == ' '){
      if(start != -1)
        ans += str.substr(start, counter);
      start = -1;
      counter = 0;
      ans+=str[i];
      continue;
    }
    start = i;
    counter++;
  }
  if(start != -1)
    ans += str.substr(start, counter);
  return ans;
}
```
### Minimum Characters For Words

#### - CPP Solution
```cpp
#include <vector>
using namespace std;

vector<char> minimumCharactersForWords(vector<string> words) {
  // Write your code here.
  vector<char> ans;
  unordered_map<char,int>dic;
  for(int i=0;i<words.size();i++){
    unordered_map<char,int>m;
    for(int j=0;j<words[i].size();j++)
      m[words[i][j]]++;
    for(auto [key,value] : m)
      if(m[key] - dic[key] > 0)
        dic[key] = m[key];
  }
  for(auto [key,value] : dic)
    for(int i=0;i<value;i++)
      ans.push_back(key);
  return ans;
}
```
### One Edit

#### - CPP Solution
```cpp
using namespace std;


bool oneEdit(string s1, string s2) {
  int count = s1.size() != s2.size()?1:0;
  if(s1.size()<s2.size()){
    swap(s1,s2);
  }
  if(s1.size()-s2.size()>1){
    return false;
  }
  for(int i=0;i<s2.size();i++){
    if(s1[i] != s2[i]){
      if(s1.size() != s2.size()){
        if(s1[i+1] != s2[i])
          count++;
        else
          s1.erase(i, 1);
      }else{
        count++;
      }
    }
    if(count > 1)
      return false;
  }
  return true;
}
```
### Longest Substring Without Duplication 

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static String longestSubstringWithoutDuplication(String str) {
        int[] indices = new int[]{0,0};
        int n = str.length();
        Map<Character,Integer> lastSeen = new HashMap<>();
        int startInd = 0;
        for(int i=0;i<n;i++){
            char c = str.charAt(i);
            if(lastSeen.containsKey(c))
                startInd = Math.max(startInd,lastSeen.get(c)+1);
            lastSeen.put(c,i);

            if(indices[1]-indices[0]<i-startInd){
                indices[0] = startInd;
                indices[1] = i;
            }
        }
        return str.substring(indices[0],indices[1]+1);
    }
}
```
### Underscorify Substring

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static String underscorifySubstring(String str, String substring) {
        // Write your code here.
        ArrayList<List<Integer>> location = collapse(getLocation(str,substring));
        StringBuilder stringBuilder = new StringBuilder();
        int idx = !location.isEmpty() ? 0 : -1;
        for(int i=0;i<str.length();i++){
            if(idx != -1){
                if(i == location.get(idx).get(0)){
                    stringBuilder.append('_');
                    stringBuilder.append(str.charAt(i));
                    if (i == location.get(idx).get(1)-1) {
                        stringBuilder.append('_');
                        idx = idx + 1 < location.size() ? idx + 1 : -1;
                    }
                } else if (i == location.get(idx).get(1)-1) {
                    stringBuilder.append(str.charAt(i));
                    stringBuilder.append('_');
                    idx = idx+1 < location.size() ? idx+1 : -1;
                }else{
                    stringBuilder.append(str.charAt(i));
                }
            }else
                stringBuilder.append(str.charAt(i));
        }
        return stringBuilder.toString();
    }

    private static ArrayList<List<Integer>> collapse(ArrayList<List<Integer>> location) {
        ArrayList<List<Integer>> newLocation = new ArrayList<>();
        if(!location.isEmpty()){
            newLocation.add(location.get(0));
            List<Integer> prev = newLocation.get(0);
            for(int i=1;i<location.size();i++){
                List<Integer> current = location.get(i);
                if(current.get(0) <= prev.get(1)){
                    prev.set(1,current.get(1));
                }else{
                    newLocation.add(current);
                    prev = current;
                }
            }
        }
        return newLocation;
    }

    private static ArrayList<List<Integer>> getLocation(String str, String substring) {
        ArrayList<List<Integer>> location = new ArrayList<>();
        int subLen = substring.length();
        for(int i=0;i<str.length();){
            int index = str.indexOf(substring,i);
            if(index == -1)
                break;
            location.add(Arrays.asList(index,index+subLen));
            i = index+1;
        }
        return location;
    }
}
```
### Pattern Matcher

#### - JAVA Solution
```java
import java.util.*;

class Program {

    public static String[] patternMatcher(String pattern, String str) {
        // Write your code here.
        boolean isSwapped = false,isYFound=false;
        int xs = 0,ys = 0,firstY=-1;
        if(pattern.charAt(0) == 'y'){
            StringBuilder stringBuilder = new StringBuilder();
            isSwapped = true;
            for(int i=0;i<pattern.length();i++){
                if(pattern.charAt(i) == 'y')
                    stringBuilder.append('x');
                else
                    stringBuilder.append('y');
            }
            pattern = stringBuilder.toString();
        }
        for(int i=0;i<pattern.length();i++){
            if(pattern.charAt(i) == 'y') {
                if(!isYFound){
                    firstY = i;
                    isYFound = true;
                }
                ys++;
            }else
                xs++;
        }
        for(int xlen=1;xlen<=str.length();xlen++){
            String x = str.substring(0,xlen);
            if(ys > 0){
                double ylen = (double) (str.length() - xlen * xs) /ys;
                if(ylen <= 0 || ylen%1 != 0)
                    continue;
                int yIdx = firstY*xlen;
                String y = str.substring(yIdx,yIdx+(int) ylen);
                String strGeneration = generatePattern(pattern,x,y);
                if(strGeneration.equals(str))
                    return isSwapped ? new String[] {y,x}:new String[] {x,y};
            }else{
                if(xlen*xs == str.length()){
                    String strGeneration = generatePattern(pattern,x,"");
                    if(strGeneration.equals(str))
                        return isSwapped ? new String[] {"",x}:new String[] {x,""};
                }

            }
        }
        return new String[] {};
    }

    private static String generatePattern(String pattern, String x, String y) {
        StringBuilder stringBuilder = new StringBuilder();
        for(int i=0;i<pattern.length();i++){
            if(pattern.charAt(i) == 'x')
                stringBuilder.append(x);
            else
                stringBuilder.append(y);
        }
        return stringBuilder.toString();
    }
}
```
### Smallest Substring Containing

#### - CPP Solution
```cpp
using namespace std;
string getValidSubString(unordered_map<char,int> dic,string str,int st,int sz){
  string ans = "";
  for(int i =st;i<str.size() and sz>0;i++){
    ans+=str[i];
    if(dic[str[i]]){
      sz--;
      dic[str[i]]--;
    }
  }
  return sz == 0 ? ans:"";
}
string smallestSubstringContaining(string bigString, string smallString) {
  string ans = "";
  int n = smallString.size();
  unordered_map<char,int> dic;
  for(int i=0;i<smallString.size();i++)
    dic[smallString[i]]++;
  for(int i=0;i<bigString.size();i++){
    if(dic[bigString[i]]){
      string sol = getValidSubString(dic,bigString,i,n);
      if(sol == "")
        continue;
      if(ans == "")
        ans = sol;
      else
        ans = ans.size()>sol.size() ? sol:ans;
    }
  }
  return ans;
}
```
### another approach

#### - CPP Solution
```cpp
using namespace std;

string smallestSubstringContaining(string bigString, string smallString) {
  int l=0,r=0;
  unordered_map<char,int> dic;
  for(int i=0;i<smallString.size();i++)
    dic[smallString[i]]++;
  for(int i=0;i<bigString.size();i++){
    if(dic[bigString[i]]){
      string sol = getValidSubString(dic,bigString,i,n);
      if(sol == "")
        continue;
      if(ans == "")
        ans = sol;
      else
        ans = ans.size()>sol.size() ? sol:ans;
    }
  }
  return "";
}
```
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
