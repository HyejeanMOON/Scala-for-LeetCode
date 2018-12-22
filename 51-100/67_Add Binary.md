Given two binary strings, return their sum (also a binary string).

For example,
a = "11"
b = "1"
Return "100".

### 解题思路
用最笨的模式匹配的方法。一定要考虑进位的问题。
#### Scala
```scala
object Solution {
    def addBinary(a: String, b: String): String = {
        var aleng = a.length
        var bleng = b.length
        var tempA = a
        var tempB = b
        if(aleng > bleng){
            var diff = aleng - bleng
            for(i <- 0 until diff){
                tempB = "0" + tempB
            }
        }
        if(aleng < bleng){
            var diff = bleng - aleng
            for(i <- 0 until diff){
                tempA = "0" + tempA
            }
        }
        var add = 0
        var res = ""
        for(i <- 0 until tempA.length){       
            var aStr = tempA.charAt(tempA.length-1-i).toString
            var bStr = tempB.charAt(tempA.length-1-i).toString
            //println(aStr)
            //println(bStr)
            if(aStr == "0" && bStr == "0"){
                if(add == 1){
                    res = "1" + res
                    add = 0
                }
                else if(add == 0){
                    res = "0" + res
                    add = 0
                }
            }
            else if((aStr == "1" && bStr == "0") ||(aStr == "0" && bStr == "1")){
                if(add == 1){
                    res = "0" + res
                    add = 1
                }
                else if(add == 0){
                    res = "1" + res
                    add = 0
                }
            }
            else if(aStr == "1" && bStr == "1" ){
                if(add == 1){
                    res = "1" + res
                    add = 1
                    //println(res)
                }
                else if(add == 0){
                    res = "0" + res
                    add = 1
                }
            }
        }
        //println(res)
        if(add == 1){
            res = "1" + res
        }
        res
    }
}
```