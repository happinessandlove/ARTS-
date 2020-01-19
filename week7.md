# 1. Algorithm
>[14. 最长公共前缀](https://leetcode-cn.com/problems/longest-common-prefix/)<br>
``` java
 public static String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) {
            return "";
        }
        int[] point = new int[strs.length];
        int result = -1;
        boolean allHave = true;
        for (int j = 0; j < strs[0].length(); j++) {
            allHave = true;
            for (int i = 1; i < strs.length; i++) {
                if ((j + 1) > strs[i].length()) {
                    allHave = false;
                    break;
                }
                if (!strs[i].substring(0, j + 1).equals(strs[0].substring(0, j + 1))) {
                    allHave = false;
                }
            }
            if (allHave) {
                result = j;
            } else {
                break;
            }
        }
        if (result == -1) {
            return "";
        } else {
            return strs[0].substring(0, result + 1);
        }
    }
```
# 2. Review
我们在写程序中经常会创建很多类，但事实上很多类是重复的，并且是可以重复利用的，下面给出集中常见的类滥用的例子。
##### 错误示范1:
``` java
String s = new String("bikini");
```
##### 正确示范1:
``` java
String s = "bikini";
```
##### 错误原因:
###### 错误示范中如果在循环或方法中被重复调用，会重复创建对象，而正确示范则不会，只会有一个"bikini"。
---
##### 错误示范2:
``` java
static boolean isRomanNumeral(String s) {
        return s.matches("^(?=.)M*(C[MD]|D?C{0,3})" + "(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");
    }
```
##### 正确示范2:
``` java
public class RomanNumerals {
        private static final Pattern ROMAN = Pattern.compile("^(?=.)M*(C[MD]|D?C{0,3})" + "(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");

        static boolean isRomanNumeral(String s) {
            return ROMAN.matcher(s).matches();
        }
    }
 ```
 ##### 错误原因:
 ###### 错误示范中每次调用matches函数都会创建一个Pattern对象，并且只会用一次。
---
 ##### 错误示范3:
 ``` java
 private static long sum() {
        Long sum = 0L;
        for (long i = 0; i <= Integer.MAX_VALUE; i++) {
             sum += i;
        }
        return sum;
    }
 ```
 ##### 正确示范3:
 ``` java
 private static long sum() {
        long sum = 0L;
        for (long i = 0; i <= Integer.MAX_VALUE; i++) sum += i;
        return sum;
    }
 ```
##### 错误原因:
###### 错误示范中每次进行累加时都会进行拆箱和装箱操作，会耗费性能。
# 3. Tips
这次分享的技巧鸟哥的Linux私房菜:
![知识图](http://images.zhuhuajiancai.top/Mind%20Map%203.png)
>[文章链接](http://linux.vbird.org/linux_basic/0410accountmanager.php#account)

# 4. Share
数据分析渐渐成为各行各业的从业者的必备能力，数据分析主要包括以下几个典型步骤：商业理解->数据理解->数据准备与清洗->建模->模型评估->部署上线。这些东西对于没有编程基础或者是不是数据分析领域的开发人员来说都是比较困难的。IBM云提供了图形化的界面让你快速完成以上步骤，同时也提供Notebooks给专业人士进行在线编码。下面是入门指导，一共5篇文章。
>[入门指导](https://developer.ibm.com/articles/introduction-watson-studio/)
