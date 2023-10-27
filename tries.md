## Trie problems

### Suffix Trie Construction

#### - JAVA Solution
```java
import java.util.*;

class Program {
  // Do not edit the class below except for the
  // populateSuffixTrieFrom and contains methods.
  // Feel free to add new properties and methods
  // to the class.
  static class TrieNode {
    Map<Character, TrieNode> children = new HashMap<Character, TrieNode>();
    boolean endWord = false;
  }

  static class SuffixTrie {
    TrieNode root = new TrieNode();
    char endSymbol = '*';

    public SuffixTrie(String str) {
      populateSuffixTrieFrom(str);
    }

    public void populateSuffixTrieFrom(String str) {
      for(int i=0;i<str.length();i++)
        insert(i,str);
    }
    void insert(int start,String str) {
      TrieNode curr = root;
      for(int i=start;i<str.length();i++){
        char c = str.charAt(i);
        if(curr.children.get(c) == null)
          curr.children.put(c, new TrieNode());
        curr = curr.children.get(c);
      }
      curr.children.put(this.endSymbol, null);
      curr.endWord = true;
    }

    public boolean contains(String str) {
      TrieNode curr = root;
      for(int i=0;i<str.length();i++){
        char c = str.charAt(i);
        if(curr.children.get(c) == null)
          return false;
        curr = curr.children.get(c);
      }
      return curr.endWord;
    }
  }

}
```
### Multi String Search

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public static List<Boolean> multiStringSearch(
            String bigString, String[] smallStrings
    ) {
        SuffixTrie suffixTrie = new SuffixTrie();
        suffixTrie.populateString(bigString);
        ArrayList<Boolean> searchResults = new ArrayList<>();
        for(String str:smallStrings)
            searchResults.add(suffixTrie.contain(str));
        return searchResults;
    }
    static class Trie{
        Map<Character,Trie> children = new HashMap<>();
    }

    static class SuffixTrie{
        Trie root = new Trie();

        void populateString(String str){
            for(int i=0;i<str.length();i++)
                insert(i,str);
        }
        void insert(int i,String str){
            Trie curr = root;
            for(;i<str.length();i++){
                if(!curr.children.containsKey(str.charAt(i)))
                    curr.children.put(str.charAt(i),new Trie());
                curr =  curr.children.get(str.charAt(i));
            }
        }

        boolean contain(String str){
            Trie curr = root;
            for(int i=0;i<str.length();i++){
                char c = str.charAt(i);
                if(curr == null || !curr.children.containsKey(c))
                    return false;
                curr = curr.children.get(c);
            }
            return true;
        }
    }
}
```
### Longest Most Frequent Prefix

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public String longestMostFrequentPrefix(String[] strings) {
        // Write your code here.
        Trie trie = new Trie();
        for(String word:strings)
            trie.insert(word);
        
        return trie.fullString.substring(0, trie.maxPrefixLength);
    }
    class Node{
        Map<Character,Node> children = new HashMap<>();
        int count = 0;
    }
    class Trie{
        Node root = new Node();
        int maxPrefixCount = 0 ;
        int maxPrefixLength = 0;
        String fullString = "";
        void insert(String str){
            Node curr = root;
            for(int i=0;i<str.length();i++){
                char c = str.charAt(i);
                if(!curr.children.containsKey(c))
                    curr.children.put(c,new Node());
                curr =  curr.children.get(c);
                curr.count++;
                if(curr.count>maxPrefixCount){
                    maxPrefixLength = i+1;
                    fullString = str;
                    maxPrefixCount = curr.count;
                } else if(curr.count == maxPrefixCount && maxPrefixLength < i+1) {
                    maxPrefixLength = i+1;
                    fullString = str;
                }
            }
        }
    }
}
```
### Shortest Unique Prefixes

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public String[] shortestUniquePrefixes(String[] strings) {
        // Write your code here.
        Trie trie = new Trie();
        for(String word:strings)
            trie.insert(word);
        String[] shortest = new String[strings.length];
        for (int i=0;i< strings.length;i++)
            shortest[i] = trie.containUniquePrefix(strings[i]);
        return shortest;
    }
    class Node{
        Map<Character,Node> children = new HashMap<>();
        int count = 0;
    }
    class Trie{
        Node root = new Node();
        void insert(String str){
            Node curr = root;
            for(int i=0;i<str.length();i++){
                char c = str.charAt(i);
                if(!curr.children.containsKey(c))
                    curr.children.put(c,new Node());
                curr =  curr.children.get(c);
                curr.count++;
            }
        }
        String containUniquePrefix(String str){
            Node curr = root;
            int countSubStringSize = 0;
            while(countSubStringSize<str.length()-1){
                char c = str.charAt(countSubStringSize);
                curr = curr.children.get(c);
                if(curr.count == 1)
                    break;
                countSubStringSize++;
            }
            return str.substring(0,countSubStringSize+1);
        }
    }
}
```
### Strings Made Up Of Strings

#### - JAVA Solution
```java
import java.util.*;

class Program {
    public String[] stringsMadeUpOfStrings(
            String[] strings, String[] substrings
    ) {
        // Write your code here.
        Trie trie = new Trie();
        List<String> out = new ArrayList<>();
        for(int i=0;i< substrings.length;i++)
            trie.insert(substrings[i]);
        for(int i=0;i< strings.length;i++)
            if(trie.contain(strings[i],0,new HashMap<>()))
                out.add(strings[i]);
        return out.toArray(new String[out.size()]);
    }
    class Node{
        Map<Character,Node> children = new HashMap<>();
        boolean endWord;
    }
    class Trie{
        Node root = new Node();
        void insert(String str){
            Node curr = root;
            for(int i=0;i<str.length();i++){
                char c = str.charAt(i);
                if(!curr.children.containsKey(c))
                    curr.children.put(c,new Node());
                curr =  curr.children.get(c);
            }
            curr.endWord = true;
        }

        public boolean contain(String string,int startIdx,HashMap<Integer,Boolean> memo) {
            if(startIdx == string.length())
                return true;
            if(memo.containsKey(startIdx))
                return memo.get(startIdx);
            Node curr = root;
            for (int i =startIdx;i<string.length();i++){
                char c = string.charAt(i);
                if(!curr.children.containsKey(c))
                    break;
                curr = curr.children.get(c);
                if(curr.endWord && contain(string,i+1,memo)){
                    memo.put(startIdx,true);
                    return true;
                }
            }
            memo.put(startIdx,false);
            return false;
        }
    }
}
```
