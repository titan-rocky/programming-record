### Coin Change (Counting ways)
```cpp
class Solution {
  public:
    int count(vector<int>& coins, int sum) {
        int n = coins.size();
        vector<int> dp (sum+1,0);
        for (int coin: coins){
            for (int j=1; j<=sum; j++){
                if (j-coin<0) continue;
                else if (j-coin==0) dp[j]+=1;
                else {
                    dp[j] += dp[j-coin];
                }
            }
        }
        return dp[sum];
    }
};
```

2D DP: `dp[i][j]=dp[i-1][j]+dp[i][j-coin]`
**1D DP:** Replacing on same for every coin `dp[i]+=dp[i-coin]`

![[Pasted image 20241114185715.png]]

Time Complexity: $O(n*sum)$
Space Complexity: $O(sum)$

### First and Last Occurences
```cpp
class Solution {
  public:
    int binsearch_l(vector<int> &arr, int val){
        int n = arr.size(); int l=0, r=n-1, m=0, res=-1;
        while (l<=r){
            m = (l+r)/2;
            if (arr[m]>=val) {
                if (arr[m]==val) res=m;
                r = m-1;
            }
            else l=m+1;
        }
        return res;
    }
    int binsearch_r(vector<int> &arr, int val){
        int n = arr.size(); int l=0, r=n-1, m=0, res=-1;
        while (l<=r){
            m = (l+r)/2;
            if (arr[m]>val) r = m-1;
            else {
                if (arr[m]==val) res=m;
                l=m+1;
            }
        }
        return res;
    }
    vector<int> find(vector<int>& arr, int x) {
        int first = binsearch_l(arr,x);
        int last = binsearch_r(arr,x);
        return {first,last};
    }
};
```

![[Pasted image 20241114194214.png]]

Time Complexity: $O(log(N))$
Space Complexity: $O(1)$

### Find Transition Point
```cpp
class Solution {
  public:
    int transitionPoint(vector<int>& arr) {
        int n = arr.size();
        int l=0, r=n-1, m=0, res=-1;
        while (l<=r){
            m = (l+r)/2;
            if (arr[m]==1) {r=m-1; res=m;}
            else l=m+1;
        }
        return res;
    }
};
```

![[Pasted image 20241114195236.png]]

Time Complexity: $O(log(N))$
Space Complexity: $O(1)$

### First Repeating Element
```cpp
class Solution {
  public:
    // Function to return the position of the first repeating element.
    int firstRepeated(vector<int> &arr) {
        unordered_map<int,int> mp;
        int i=1, mv=INT_MAX, rep_index=1e6+5;
        for (int val: arr){
            if (mp[val]) {
                rep_index=min(rep_index,mp[val]);
            }
            mp[val] = i++;
        }
        return (rep_index==1e6+5?-1:rep_index);
    }
};
```

![[Pasted image 20241114213731.png]]

Time Complexity: $O(N)$
Space Complexity: $O(N)$

### Remove Duplicates sorted array
```cpp
class Solution {
  public:
    int remove_duplicate(vector<int> &arr) {
        auto i = arr.begin();
        int n = arr.size(), el = -1, rep=0;
        while (i!=arr.end()){
            if (el==arr[i-arr.begin()]) {i=arr.erase(i);rep++;}
            else {el=arr[i-arr.begin()];i++;}
        }
        return n-rep;
    }
};
```

Time Complexity: $O(N)$
Space Complexity: $O(1)$
