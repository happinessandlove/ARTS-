# 1. Algorithm
7. 整数反转
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
在使用不可实例化的类时，强制使用私有构造方法，这样这个工具类就不可以进行实例化。
``` java
public class UtilityClass {
        private UtilityClass() {
            throw new AssertionError();
        }
    }
```
##### 好处：
1. 保证该类在任何情况下都不能被实例化
2. 不误导使用者认为该类的使用需要实例化
##### 缺点：
1. 该类不可以被继承
# 3. Tips
这次分享的技巧是如何在java中优雅处理lambda表达式异常。众所周知，lambda表达式可以使代码更加简洁，但是在处理异常时却需要加上try catch这种代码，使得代码又变的啰嗦，这里提供了一个方法以解决这种问题。
``` java
@FunctionalInterface
public interface HandlingConsumer <Target, ExObj extends Exception>{
    void accept(Target target) throws ExObj;
    static <Target> Consumer<Target> handlingConsumerBuilder(
            HandlingConsumer<Target, Exception> handlingConsumer) {
        return obj -> {
            try {
                handlingConsumer.accept(obj);
            } catch (Exception ex) {
                throw new RuntimeException(ex);
            }
        };
    }
}
```
测试用例
``` java 
public class HandlingConsumerTest {
    @Test
    public void accept() {
        List<Integer> list = Arrays.asList(5, 4, 3, 2, 1);
        Assertions.assertDoesNotThrow(() -> list.forEach(handlingConsumerBuilder(i -> Thread.sleep(i))));
        Assertions.assertThrows(RuntimeException.class, () -> list.forEach(handlingConsumerBuilder(i -> Thread.sleep(i))));
    }
}
```

# 4. Share
这次分享一个youtube 上的一个视频，主题是在学习编程时如何保持动力。在视频中up主分享了他在学习编程时的经历：他在0基础学习制作一个复杂app时遇到了很多困难，他从网上复制粘贴代码，然后遇到问题就谷歌，但这效率很低，并且有时候就算找到了解决方案他也无法实现，因此他认识到了基础的重要性，他花了两周时间通过《head first Java》这本书以补充基础。他总结说，如果他之前能够花费一周的时间来学习基础知识的话，那么他在解决问题的时候就能节省很多时间。他在视频的最后说明了激情和动力的区别。激情可能会让你今天对编程很有兴趣，但是第二天随着激情的减少，可能你就不想做了，所以最重要的是要知道你为何出发，找到你原始动力这样才能够持续地进步。
>[视频链接](https://youtu.be/oyk0WPTQlhg)
