

# [Strivers A2Z DSA Course/Sheet](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/)


## Arrays
### Easy

#### 1. Largest Element in Array


```java
class Compute {
    
    public int largest(int arr[], int n)
    {
        int max=Integer.MIN_VALUE;
        for(int a:arr){
            if(a>max){
                max=a;
            }
        }
        return max;
        
    }
}
```

#### 2. Second Largest

```java
class Solution {
    int print2largest(int arr[], int n) {
        
        int max1=-1;
        int max2=-1;
        
        for(int i:arr){
            if(i>max1){
                max2=max1;
                max1=i;
            }else if(i>max2 && i!=max1){
                max2=i;
            }
        }
        return max2;
    }
}
```

#### 3. Check if array is sorted

```java
class Solution {
    boolean arraySortedOrNot(int[] arr, int n) {
        for(int i=1;i<n;i++){
            if(!(arr[i]>=arr[i-1])){
                return false;
            }
        }
        return true;
    }
}
```

#### 4. Quick Left Rotation

#### Reversal Approach


```java 
import java.util.*;

class Main {
  public static void leftRotate(int arr[], int k, int n) {
    reverseArray(arr, 0, k - 1);
    reverseArray(arr, k, n - 1);
    reverseArray(arr, 0, n - 1);
  }

  static void reverseArray(int arr[], int start, int end) {
    int temp;
    while (start < end) {
      temp = arr[start];
      arr[start] = arr[end];
      arr[end] = temp;
      start++;
      end--;
    }
  }
}
```
#### Juggling Algorithm
```java
import java.util.*;

class Main {
  public static void leftRotate(int arr[], int k, int n) {
    int i, j, d, temp;
    for (i = 0; i < gcd(k, n); i++) {
      temp = arr[i];
      j = i;
      while (true) {
        d = (j + k) % n;
        if (d == i) {
          break;
        }
        arr[j] = arr[d];
        j = d;
      }
      arr[j] = temp;
    }
  }

  static int gcd(int a, int b) {
    if (b == 0) {
      return a;
    } else {
      return gcd(b, a % b);
    }
  }
}
```

There are some trade-offs between the ```Juggling algorithm``` and the ```Reversal algorithm``` that could influence which one is preferred in a specific use case:

*Code Complexity:* The Juggling algorithm requires a
separate gcd function to calculate the greatest common divisor of k and n. The Reversal algorithm, on the other hand, is more compact and doesn't require a separate gcd function. So if code simplicity and readability are a concern, the Reversal algorithm may be preferred.

*Intuition:* The Juggling algorithm is more intuitive and easy to understand. It is a straightforward approach that rotates elements of the array by swapping the values. The Reversal algorithm, on the other hand, requires a bit more mental effort to understand as it involves reversing the sub-arrays. If intuition and ease of understanding are a concern, the Juggling algorithm may be preferred.

*Memory Usage:* Both algorithms have the same memory usage, as they do not require any additional memory allocation other than the input array.

*Edge Cases:* There are no specific edge cases where one algorithm must be used over the other. Both algorithms work for all cases and produce the same results.

In summary, the choice between the Juggling algorithm and the Reversal algorithm depends on the specific use case and the context of the problem. Both algorithms are `O(N)` in time complexity and produce the same results, so it's recommended to choose the algorithm that you find the most readable, maintainable, and easy to understand for your specific use case.


#### 5. Move all zeroes to end of array
```java
class Solution {
    void pushZerosToEnd(int[] arr, int n) {
        // code here
    int count=0;
    
    for(int i=0;i<n;i++){
        if(arr[i]!=0){
            arr[count++]=arr[i];
        }
    }
    while(count<n){
        arr[count++]=0;
    }
    
    }
}
```

#### 6. Searching an element in a sorted array
```java
class Solution{
    static int searchInSorted(int arr[], int N, int K)
    { 
        // Your code here
        int low=0;
        int high=N-1;
        while(low<=high){
            int mid=(low+high)/2;
            if(arr[mid]==K){
                return 1;
            }else if(arr[mid]<K){
                low=mid+1;
            }else{
                high=mid-1;
            }
            
        }
        return -1;  
    }
}
```

#### 7. Union of Two Sorted Arrays

```java
class Solution
{
    //Function to return a list containing the union of the two arrays.
    public static ArrayList<Integer> findUnion(int arr1[], int arr2[], int n, int m)
    {
        // add your code here
        ArrayList<Integer> ans=new ArrayList<>();
        
        int i=0;
        int j=0;
        while(i<n && j<m){
            if(arr1[i]==arr2[j]){
                if(ans.size()==0 || ans.get(ans.size()-1)!=arr1[i]){
                ans.add(arr1[i]);
                }
                i++;
                j++;
            }else if(arr1[i]<arr2[j]){
                if(ans.size()==0 || ans.get(ans.size()-1)!=arr1[i]){
                    ans.add(arr1[i]);
                }
                i++;
            }else if(arr1[i]>arr2[j]){
                if(ans.size()==0 || ans.get(ans.size()-1)!=arr2[j]){
                    ans.add(arr2[j]);
                }
                j++;
            }
        }
        while(i<n){
            if(ans.get(ans.size()-1)!=arr1[i]){
                    ans.add(arr1[i]);
                }
                i++;
        }
        while(j<m){
            if(ans.get(ans.size()-1)!=arr2[j]){
                    ans.add(arr2[j]);
                }
                j++;
        }
        return ans;
    }
}
```

#### 8. Missing number
```java
class Compute {
    
    public static int missingNumber(int A[], int N)
    {
         // Your code goes here
         int sum=0;
         for(int i:A){
             sum+=i;
         }
         int exp=(N*(N+1))/2;
         return exp-sum;
    }
}
```

#### 9. Maximize Number of 1's
#### Flipping m zeroes 
```java
class Solve {
    // m is maximum of number zeroes allowed to flip
    int findZeroes(int arr[], int n, int m) {
        
        int start=0;
        int zeroCount=0;
        int max=0;
        for(int i=0;i<n;i++){
            if(arr[i]==0){
                zeroCount++;
            }
            while(zeroCount>m){
                if(arr[start]==0){
                    zeroCount--;
                }
                start++;
            }
            max=Math.max(max,i-start+1);
        }
        return max;
    }
}
```
#### Max Consecutive Ones
```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int max=0;
        int count=0;
        for(int i=0;i<nums.length;i++){
            if(nums[i]!=0){
                count++;
            }else{
                count=0;
            }
            max=Math.max(max,count);
        }
        return max;
    }
}
```

#### 10. Longest Sub-Array with Sum K
```java
class Solution{

    // Function for finding maximum and value pair
    public static int lenOfLongSubarr (int A[], int N, int K) {
        //Complete the function
        
        int start=0;
        int sum=0;
        int max=0;
        
        Map<Integer,Integer> mp=new HashMap<Integer,Integer>();
        
        for(int i=0;i<N;i++){
            sum += A[i];
            
            if(mp.containsKey(sum-K)){
                int plen=i-mp.get(sum-K);
                max=Math.max(max,plen);
            }
            if(mp.containsKey(sum)==false){
                mp.put(sum,i);
            }
            if(sum==K){
                max=Math.max(max,i+1);
            }
        }
        
        return max;
    }
    
    
}
```

```
class Solution{

    // Function for finding maximum and value pair
    public static int lenOfLongSubarr (int A[], int N, int K) {
        int start=0;
        int sum=0;
        int max=0;
        
        for(int i=0;i<N;i++){
            sum+=A[i];
            while(sum>K && start<=i){
                sum-=A[start];
                start++;
            }
            if(sum==K){
                max=Math.max(max,i-start+1);
            }
         }
         return max;
    }
}
```
Both approaches have the same time complexity of ```O(n)``` and solve the same problem. However, the choice of which approach to use may depend on several factors, such as:

*Space Complexity:* If space complexity is a concern, the second approach without a hash map is preferable as it has a constant space complexity. The first approach using a hash map has a linear space complexity.

*Readability:* Depending on the development team and the coding style, one approach may be more readable than the other. The first approach using a hash map is more straightforward and easier to understand for some, while the second approach is more concise and efficient.

*Development Environment:* If the development environment requires strict coding standards or disallows the use of hash maps, the second approach without a hash map is a better choice.

In conclusion, both approaches have their strengths and weaknesses, and the choice of which to use depends on the specific requirements and constraints of the project.

    > If Array elements consists of negative numbers then Two Pointers apporoach won't work Go with HashMap apporoach 

#### 11. Find the element that appears once
```java
class Solution {
    public int singleNumber(int[] nums) {
        
        int xor=0;
        for(int i:nums){
            xor^=i;
        }
        return xor;
    }
}
```
    >>> Time : O(N)

##### If the Arrays is sorted then we can choose Binary Searching approach and can do it in `O(Log(N))`

```java
class Sol
{
    public static int search(int A[], int N)
    {
        int left = 0;
        int right = A.length - 1;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (mid % 2 == 0) {
                if (A[mid] == A[mid + 1]) {
                    left = mid + 2;
                } else {
                    right = mid;
                }
            } else {
                if (A[mid] == A[mid - 1]) {
                left = mid + 1;
                } else {
                right = mid - 1;
                }
            } 
        }
        return A[left];
    }
}
```
#### 12. Search in a 2D matrix
```java
class Sol
{
    public static int matSearch(int mat[][], int N, int M, int X)
    {
        // your code here
        int i=0;
        int j=M-1;
        while(i<N && j>=0){
            if(mat[i][j]==X){
                return 1;
            }
            
            if(mat[i][j]>X){
                j--;
            }else{
                i++;
            }
        }
        return 0;
    }
}
```

#### 13. Row with max 1s
```java
class Solution {
    int rowWithMax1s(int arr[][], int n, int m) {
        // code here
       int maxOnes = 0;
    int maxOnesRow = -1;
    int ones = 0;
    for (int i = 0; i < n; i++) {
        int j = 0;
        while (j < m && arr[i][j] == 0) {
            j++;
        }
        ones = m - j;
        if (ones > maxOnes) {
            maxOnes = ones;
            maxOnesRow = i;
        }
    }
    return maxOnesRow;
    }
}
```







