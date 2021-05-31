  fun isHappy(Array: IntArray) : Boolean{
        for(i in 1..Array.size-2) {
            if (Array[i] > (Array[i - 1] + Array[i + 1]))
                return false
        }
        return true
    }
    fun makeHappy(sadArray: IntArray): IntArray{
        var temp = IntArray(sadArray.size)
        temp[0] = sadArray[0]
        var offset = 0
        for(i in 1..sadArray.size-2)
        {
            if(sadArray[i] <= (sadArray[i-1]+sadArray[i+1]))
                temp[i-offset] = sadArray[i]
            else
                offset++
        }
        temp[sadArray.size-offset-1] = sadArray[sadArray.size-1]
        return (temp.filter{it>0}).toIntArray()
    }
    fun convertToHappy(sadArray: IntArray): IntArray {
        throw NotImplementedError("Not implemented")
    var tmp = sadArray
        while(!isHappy(tmp))
            tmp = makeHappy(tmp)
        return tmp
    }
}



class StringParser {
    // TODO: Complete the following function
    fun getResult(inputString: String): Array<String> {
        throw NotImplementedError("Not implemented")
        val characterOpnArr = charArrayOf('<','(','[')
        val characterEndArr = charArrayOf('>',')',']')
        var result = ArrayList<String>()
        var flag = false
        var flagIndices : Int=0
        var pos : Int = 0
        var brPos: Int = 0
        var clone=0
        while(pos <= inputString.length-1){
            var word = inputString[pos++]
            if(word in characterOpnArr && !flag ) {
                flag=true
                brPos = pos++
                flagIndices = characterOpnArr.indexOf(word)
            }
            else if(word == characterOpnArr[flagIndices] && flag){
                clone ++
            }
            else if(word ==characterEndArr[flagIndices] && clone>0) {
                clone--
                pos++
            }
            else if(word in characterEndArr && flag && word==characterEndArr[flagIndices]){
                result.add(inputString.substring(brPos,pos-1))
                pos = brPos++
                flag = false
            }
        }
        return result.toTypedArray()
    }
}
