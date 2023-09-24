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
