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
