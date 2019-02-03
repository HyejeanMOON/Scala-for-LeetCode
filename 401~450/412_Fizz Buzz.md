Write a program that outputs the string representation of numbers from 1 to n.

But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.

Example:
```
n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
```

### 解题思路
#### Scala
```scala
object Solution {
    def fizzBuzz(n: Int): List[String] = {
        var res:List[String] = List()
        for(i <- 1 to n){
            if(i%3==0){
                if(i%5!=0){
                    res = res :+ "Fizz"
                }else{
                    res = res :+ "FizzBuzz"
                }
            }else if(i%5==0){
                res = res :+ "Buzz"
            }else{
                res = res :+ i.toString
            }
        }
        res
    }
}
```