# Algorithm

## 1.Title  
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.  

An input string is valid if:  
    1)Open brackets must be closed by the same type of brackets.  
    2)Open brackets must be closed in the correct order.  
Note that an empty string is also considered valid.  


## 2.Example  
### 2.1 Example 1
    Input: "()"
    Output: true

### 2.2 Example 2
    Input: "()[]{}"
    Output: true

### 2.3 Example 3
    Input: ([)]
    Output: false


## 3.Solution   

给出自己的解答和解题思路，以及自己对leetcode上给出的解题思路的理解

### 3.1 自己的解答,时间复杂度：O(n)，空间复杂度O(n)

解题思路：
```
1.使用栈的数据结构来控制开始括号字符的顺序，如果是开始的括号则直接压入栈中，如果不是则需要对栈中的顶部元素对比。
2.使用map集合来维护每一种字符所对应的值，这样如果是栈中的顶部元素和当前的元素是一对，则加起来和为0.
3.如果最后栈的元素为0，则是有效的字符串，否则不是有效字符串。
4.有两种情况单独做了特殊的判断：
    1）如果第一个元素为关闭的括号，则直接返回false（即栈的大小为0，且在map中对应的值小于0）
    2）如果当前元素为关闭的括号且栈的元素不为0，比较如果栈的顶部元素和当前元素和不为0，则不是有效字符串。
```
代码实现：
```
public static boolean isValidString(String s) {
        if(s == null)
            return true;

        Map<Character,Integer> map = new HashMap<>();
        map.put('{',3);
        map.put('[',2);
        map.put('(',1);
        map.put('}',-3);
        map.put(']',-2);
        map.put(')',-1);

        char[] chars = s.toCharArray();
        Stack<Character> stack = new Stack<>();
        int i = 0;
        while(i < chars.length) {
            char ch = chars[i];
            int num = map.get(ch);

            if(num < 0 && stack.size() == 0)
                return false;

            if(num < 0 && stack.size() > 0 && num + map.get(stack.peek()) != 0)
                return false;

            if(num > 0 )
                stack.push(ch);

            if(num < 0)
                stack.pop();

            i++;
        }
        if(stack.size() == 0)
            return true;
        return false;
    }
```

### 3.2 自己对leetcode解题思路的理解，时间复杂度O(n)，空间复杂度O(n)
解题思路：

```
1.使用stack数据结构控制开始括号字符的顺序，如果顶部元素与当前元素为一对，即将该顶部元素出栈
2.使用map集合维护每一对括号，其中key为关闭括号，value为开始括号
3.最后如果栈的元素为0，即为有效字符串
```
代码实现：
    
```
public boolean isVaild(String s){
        Map<Character,Character> mappings = new HashMap<>();
        mappings.put(')','(');
        mappings.put(']','[');
        mappings.put('}','{');
        Stack<Character> stack = new Stack<>();
        for(int i = 0;i< s.length();i++){
            char ch = s.charAt(i);
            if(mappings.containsKey(ch)){//此时该括号是close 的括号，需要进一步比较
                //判断close括号与栈中的open 括号是否是一对
                char topElement = stack.isEmpty()?'#':stack.pop();//stack中的对象
                if(topElement != mappings.get(ch))
                    return false;
            }else{//否则，直接放入栈中
                stack.push(ch);
            }
        }
        return stack.isEmpty();
    }
```

## 4.summary  
思路大体上是没有问题的，但是针对该题存在以下几个问题：  
首先没有考虑到在map集合中通过维护一对括号，且key是关闭括号的方式来直接判断是否是同一对括号；  
其次在代码开发中，没有注意到如果栈为空的情况下，可以通过给定一个特殊的字符表示（在我自己的里面可以用0或者其他数字表示），这样本来是同一套判断逻辑就不需要再单独拿出去做判断，因为这样别人去看你代码的时候，会觉得逻辑不清晰；  
最后就是返回结果，后续应该多注意一下java的api方法，避免代码冗余。  


# Review
这周看了别人写的一篇英文博客，阐述了servlet和JSP的区别。在整篇文章中，作者在简要描述什么是JSP、什么是servlet后，从自定义标签、定义、编码的容易程度、MVC的模式、结构、session管理、request支持等多个方面对比了jsp与servlet的区别，最后总结了servlet远远比JSP强大很多，且如果没有servlet，JSP就不会存在了。


# Tip
[如何在idea中集成git](https://blog.csdn.net/miwanmeng/article/details/81128353)  
[如果VCS中没有git该如何显示](https://blog.csdn.net/baidu_37107022/article/details/78033855)


# Share
[阿里毕玄：系统架构师如何做好系统设计](https://mp.weixin.qq.com/s/LrpvaAQSn_TITMwH7XhG3A)
