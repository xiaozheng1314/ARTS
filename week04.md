# Algorithm One

## 1.Title  
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "". 


## 2.Example  
### 2.1 Example 1
    Input: ["flower","flow","flight"]
    Output: "fl"

### 2.2 Example 2
    Input: ["dog","racecar","car"]
    Output: ""


## 3.Solution   

给出自己的解答和解题思路，以及自己对leetcode上给出的解题思路的理解

### 3.1 自己的解答,时间复杂度：O(n)，空间复杂度O(n)

代码实现：
```
 public static  String longestCommonPrefix(String[] strs) {
        if(strs == null || strs.length == 0)
            return "";

        int minLength = Integer.MAX_VALUE;
        for(int i = 0;i < strs.length; i++){
            int length = strs[i].length();
            if(minLength > length)
                minLength = length;
        }

        int index = 0;
        String first = strs[0];
        int num = strs.length;
        for(int i = 0;i < minLength;i++) {//最短的字符串
            //如果第一个字母不相等，就直接退出
            if(i > 0 && index == 0)
                continue;

            int count = 1;
            for (int j = 1; j < num; j++) {//字符串的个数
                if (strs[j].charAt(i) == first.charAt(i))
                    count++;
            }

            if (count == num) {
                index++;
            }
        }
        return index != 0 ?first.substring(0,index):"";
    }
```

### 3.2 leetcode解题思路的代码，时间复杂度O(n)，空间复杂度O(n)

代码实现：
    
```
 public static  String longestCommonPrefix1(String[] strs) {
        //time O(n)  space O(1)
        if(strs.length == 0)
            return "";
        String commonStr = strs[0];
        for (int i = 1;i < strs.length;i++){
            System.out.println(strs[i].indexOf(commonStr)+" : "+strs[i]+" indexOf "+commonStr);
            while(strs[i].indexOf(commonStr) != 0){
                //如果返回-1，则说明这个字符串中没有包含commonStr的字符串；且即使这个字符串为""，indexOf也不会报错，值仍然为-1
                //使用！= 0是为了确定这些字符串必须出现在第一位，所以不能用-1来判断是否能找到公共字符串
                commonStr = commonStr.substring(0,commonStr.length()-1);
                if(commonStr.isEmpty())
                    return "";
            }
        }
        return commonStr;
    }
```

```
 public static  String longestCommonPrefix2(String[] strs) {
        //time O(n)  space O(1)
        if(strs.length == 0 || strs == null)
            return "";
        String commonStr = strs[0];
        for (int i = 0;i < commonStr.length();i++){//遍历第一个元素的长度
            for (int j = 0 ;j < strs.length ;j++){//遍历字符串数组的每一个元素
                if(i == strs[j].length() || commonStr.charAt(i) != strs[j].charAt(i)){
                    //如果达到当前字符串的最大长度 或当前字符不相等，则除掉当前的字符外，前面的就都是相等的
                    return commonStr.substring(0,i);
                }
            }
        }
        return commonStr;
    }
```

```
 public static  String longestCommonPrefix3(String[] strs) {

        if(strs.length == 0 || strs == null)
            return "";
        return longestCommonPrefix(strs,0,strs.length-1);
    }

    private static String longestCommonPrefix(String[] strs, int index, int len) {
        if(len == index)//如果只有一个元素，就直接返回str[0]
            return strs[index];
        else{
            int mid = (len + 1) / 2;
            String lcpLeft = longestCommonPrefix(strs,1,mid);
            String lcpRight = longestCommonPrefix(strs,mid+1,len);
            return commonPrefix(lcpLeft,lcpRight);
        }
    }

    private static String commonPrefix(String lcpLeft, String lcpRight) {
        int min = Math.min(lcpLeft.length(),lcpRight.length());
        for (int i = 0;i< min;i++){
            if(lcpLeft.charAt(i) != lcpRight.charAt(i))
                return lcpLeft.substring(0,i);
        }
        return lcpRight.substring(0,min);
    }
```

```
  public static  String longestCommonPrefix4(String[] strs) {
        if(strs.length == 0 || strs == null)
            return "";
        //1.找出最小的字符串
        int minLen = Integer.MAX_VALUE;
        for (String str: strs)
            minLen = Math.min(minLen,str.length());

        //2.使用二分法，查询前半段是否其他所有字符串都包含
        int low = 1;
        int high = minLen;
        while(low <= high){
            int mid = (low + high) / 2;
            if(isCommonPrefix(strs,mid))
                low = mid + 1;
            else
                high = mid - 1;
        }
        return strs[0].substring(0,(low + high) / 2);
    }

    private static boolean isCommonPrefix(String[] strs, int len) {
        String str = strs[0].substring(0,len);
        for (int i = 1 ; i < str.length() ;i++){
            if(!strs[i].startsWith(str))
                return false;
        }
        return true;
    }
```
## 4.summary  
通过看leetcode上的解题思路，自己的思路完全就跟没有一样，后续需要继续努力啊。


# Review
看了spring的doc中描述了如何配置定时任务，以及定时任务的分类等相关的介绍。


# Tip
[还在业务中用if else，策略模式了解一下](https://mp.weixin.qq.com/s/qh5rT1eEpLtLntj827PPfw)  
根据以上文章案例，使用策略模式改写了代码，并回顾了策略模式。

# Share
[技术人具备“结构化思维”意味着什么？](https://mp.weixin.qq.com/s/LCR8s3b4WvqMdoAH1biFvw)
