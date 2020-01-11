# 1. Algorithm
7. 整数反转<br>
给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。<br>
``` java
public static int reverse(int x) {
        System.out.println(Math.pow(2, 31) - 1);
        System.out.println(- Math.pow(2, 31));
        Stack<Integer> stack = new Stack<>();
        int t = x;
        while (t != 0) {
            stack.push(t % 10);
            t = t / 10;
        }
        int size = stack.size();
        int result = 0;
        for (int i = 0; i < size; i ++) {
            result += stack.pop()*Math.pow(10,i);
        }
        if (result >= Math.pow(2, 31) - 1 || result <= - Math.pow(2, 31)){
            return 0;
        }
        return result;
}
```
# 2. Review
在我们平时的代码中，会发现一个类会依赖其它的类，如一个拼写检查的类会依赖于一个词典类，下面给出几个错误示范：
### 错误示范
##### 错误示范1:
``` java
public class SpellChecker {
    private static final Lexicon dictionary = ...;

    private SpellChecker() {
    } // 该类不可实例化

    public static boolean isValid(String word) { ...}

    public static List<String> suggestions(String typo) { ...}
}
```
##### 错误示范2:
``` java 
public class SpellChecker {
    private final Lexicon dictionary = ...;

    private SpellChecker(...) {
    }// 该类不可实例化

    public static SpellChecker INSTANCE = new SpellChecker(...);

    public boolean isValid(String word) { ...}

    public List<String> suggestions(String typo) { ...}
}
```
##### 错误示范3:
``` java 
public class SpellChecker {
    private Lexicon dictionary = ...;

    private SpellChecker(...) {
    }// 该类不可实例化
    
    public void setDictionary(Lexicon dictionary){
      this.dictionary = dictionary;
    }

    public boolean isValid(String word) { ...}

    public List<String> suggestions(String typo) { ...}
}
```
##### 缺点：
1. 以上两种写法都是假定一个拼写检查的类只会有词典，但事实上对于不同语言是有不同的词典点，很明显以上写法1和2是不支持更换词典的
2. 测试时需要一个特殊的词典进行测试，写法1和2也是不支持的
3. 为了解决上述的问题，我将dictionary字段改为非final,并提供set方法对其进行赋值，这种写法在多线程环境中会是代码发生不可预见的错误。
#### 正确示范:
``` java
public class SpellChecker {
    private final Lexicon dictionary;

    public SpellChecker(Lexicon dictionary) {
        this.dictionary = Objects.requireNonNull(dictionary);
    }

    public boolean isValid(String word) { ...}

    public List<String> suggestions(String typo) { ...}
}
```
这种写法就是通过构造方法进行依赖注入，它有如下优点：
##### 优点：
1. 可以在新建对象时选择需要依赖的对象，并且dictionary属性还是final,这在保证灵活的同事还提供了安全性。

#### 实践建议：
1. 构造方法的参数最好能够使用工厂类
2. 在java8中可以使用Supplier<T>这个接口通过lambada表达式提供需要的注入对象
# 3. Tips
这次分享的技巧是python的30个实用技巧
>[文章链接](https://medium.com/better-programming/java-stream-collectors-explained-6209a67a4c29)

# 4. Share
数据分析渐渐成为各行各业的从业者的必备能力，数据分析主要包括以下几个典型步骤：商业理解->数据理解->数据准备与清洗->建模->模型评估->部署上线。这些东西对于没有编程基础或者是不是数据分析领域的开发人员来说都是比较困难的。IBM云提供了图形化的界面让你快速完成以上步骤，同时也提供Notebooks给专业人士进行在线编码。下面是入门指导，一共5篇文章。
>[入门指导](https://developer.ibm.com/articles/introduction-watson-studio/)