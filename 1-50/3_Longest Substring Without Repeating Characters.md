Given a string, find the length of the longest substring without repeating characters.

Examples:
```
Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

Difficulty:Medium  
Total Accepted:516.7K  
Total Submissions:2.1M  
Related Topics:Hash Table, Two Pointers, String


### 解题思路
这道求最长无重复子串的题和之前那道 Isomorphic Strings 很类似，属于LeetCode的早期经典题目，博主认为是可以跟Two Sum媲美的一道题。给了我们一个字符串，让我们求最长的无重复字符的子串，注意这里是子串，不是子序列，所以必须是连续的。我们先不考虑代码怎么实现，如果给一个例子中的例子"abcabcbb"，让你手动找无重复字符的子串，该怎么找。博主会一个字符一个字符的遍历，比如a，b，c，然后又出现了一个a，那么此时就应该去掉第一次出现的a，然后继续往后，又出现了一个b，则应该去掉一次出现的b，以此类推，最终发现最长的长度为3。所以说，我们需要记录之前出现过的字符，记录的方式有很多，最常见的是统计字符出现的个数，但是这道题字符出现的位置很重要，所以我们可以使用HashMap来建立字符和其出现位置之间的映射。进一步考虑，由于字符会重复出现，到底是保存所有出现的位置呢，还是只记录一个位置？我们之前手动推导的方法实际上是维护了一个滑动窗口，窗口内的都是没有重复的字符，我们需要尽可能的扩大窗口的大小。由于窗口在不停向右滑动，所以我们只关心每个字符最后出现的位置，并建立映射。窗口的右边界就是当前遍历到的字符的位置，为了求出窗口的大小，我们需要一个变量left来指向滑动窗口的左边界，这样，如果当前遍历到的字符从未出现过，那么直接扩大右边界，如果之前出现过，那么就分两种情况，在或不在滑动窗口内，如果不在滑动窗口内，那么就没事，当前字符可以加进来，如果在的话，就需要先在滑动窗口内去掉这个已经出现过的字符了，去掉的方法并不需要将左边界left一位一位向右遍历查找，由于我们的HashMap已经保存了该重复字符最后出现的位置，所以直接移动left指针就可以了。我们维护一个结果res，每次用出现过的窗口大小来更新结果res，就可以得到最终结果啦。

这里我们可以建立一个256位大小的整型数组来代替HashMap，这样做的原因是ASCII表共能表示256个字符，所以可以记录所有字符，然后我们需要定义两个变量res和left，其中res用来记录最长无重复子串的长度，left指向该无重复子串左边的起始位置，然后我们遍历整个字符串，对于每一个遍历到的字符，如果哈希表中该字符串对应的值为0，说明没有遇到过该字符，则此时计算最长无重复子串，i - left +１，其中ｉ是最长无重复子串最右边的位置，left是最左边的位置，还有一种情况也需要计算最长无重复子串，就是当哈希表中的值小于left，这是由于此时出现过重复的字符，left的位置更新了，如果又遇到了新的字符，就要重新计算最长无重复子串。最后每次都要在哈希表中将当前字符对应的值赋值为i+1。  

这里解释下程序中那个if条件语句中为啥要有个m[s[i]] < left，我们用一个例子来说明，当输入字符串为"abbca"的时候，当i=4时，也就是即将要开始遍历最后一个字母a时，此时哈希表表中a对应1，b对应3，c对应4，left为2，即当前最长的子字符串的左边界为第二个b的位置，而第一个a已经不在当前最长的字符串的范围内了，那么对于i=4这个新进来的a，应该要加入结果中，而此时未被更新的哈希表中a为1，不是0，如果不判断它和left的关系的话，就无法更新结果，那么答案就会少一位，所以需要加m[s[i]] < left。
#### Scala
```scala
object Solution {
    def lengthOfLongestSubstring(s: String): Int = {
        var record:scala.collection.mutable.MutableList[Int]=scala.collection.mutable.MutableList[Int]()
        for(i<- 0 until 256){
            record = record:+0
        }
        var res = 0
        var left = 0
        for(i <- 0 until s.length){
            if(record(s(i))==0 || record(s(i))<left){
                res = scala.math.max(res,i-left+1)
            }else{
                left = record(s(i))
            }
            record(s(i))=i+1
        }
        res
    }
}
```