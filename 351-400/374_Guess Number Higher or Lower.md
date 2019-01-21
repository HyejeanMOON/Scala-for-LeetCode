We are playing the Guess Game. The game is as follows:

I pick a number from 1 to n. You have to guess which number I picked.

Every time you guess wrong, I'll tell you whether the number is higher or lower.

You call a pre-defined API guess(int num) which returns 3 possible results (-1, 1, or 0):
```
-1 : My number is lower  
 1 : My number is higher  
 0 : Congrats! You got it! 
 ```
Example:
```
n = 10, I pick 6.

Return 6.
```
Difficulty:Easy  
Total Accepted:70.9K  
Total Submissions:193.4K  
Related Topics:Binary Search

### 解题思路
非常普通的二分搜索题。
#### Java
```Java
/* The guess API is defined in the parent class GuessGame.
   @param num, your guess
   @return -1 if my number is lower, 1 if my number is higher, otherwise return 0
      int guess(int num); */

public class Solution extends GuessGame {
    public int guessNumber(int n) {
        int g = 2;
        int left = 0;
        int right = n;
        while(g!=0){
            int mid = left + (right-left)/2;
            g = guess(mid);
            if(g>0) left = mid + 1;
            else if(g<0) right = mid;
            else if(g==0) return mid;
        }
        return 0;
    }
}
```