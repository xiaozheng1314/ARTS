# week01

# Algorithm

# title
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

# Example
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

# Code

自己的答案

 public int[] twoSum1(int[] nums, int target) {
        int[] result = new int[2];
        for (int i = 0; i < nums.length ; i++){
            int other = target - nums[i];
            boolean flage = false;
            for(int j = i + 1;j< nums.length;j++){
                if(nums[j] == other){
                    result[0] = nums[i];
                    result[1] = nums[j];
                    flage = true;
                }
            }
            if(flage)
                break;
        }
        return result;
    }

别人的答案

 public int[] twoSum2(int[] nums, int target) {
        HashMap<Integer,Integer> map = new HashMap<>();
        for(int i = 0 ;i < nums.length ;i++){
            int complement = target - nums[i];
            if(map.containsKey(complement)){
                return new int[]{i,map.get(complement)};
            }
            map.put(nums[i],i);
        }
        throw new IllegalArgumentException("no two sum solution");
    }

# summary

	明显通过这两段的coding，能看出第二种解题的巧妙之处，希望在后面的解题过程中，加强思路和数据结构的锻炼。

# Review
	阅读了Servlet3.0 规范中的8.2.2 章节的内容，由于Servlet 3.0 引入了称之为“Web 模块部署描述符片段”的 web-fragment.xml 部署描述文件，而一个应用程序中可能会存在多个web-fragment.xml文件，这一节主要是介绍如何正确配置该配置文件的加载顺序。


# Tip
	这个是自己工作中解决问题收获的某一个知识点。
	[tomcat之cookie中的双引号](https://blog.csdn.net/qq_29340989/article/details/90346079)


# Share
 	[如何给女朋友解释什么是Linux的五种IO模型？](https://mp.weixin.qq.com/s/XzLHy41JrCV_y3BZpeTgwQ)
