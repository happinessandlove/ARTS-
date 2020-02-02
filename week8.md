# 1. Algorithm
>[26. 删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)<br>
``` java
 class Solution {
    public int removeDuplicates(int[] nums) {
         int result = nums.length;
        int length = nums.length;
       for(int i = 1;i < length;i++){
            if (nums[i] == nums[i-1]){
                // 进行移位操作
                for(int j = i+1;j < length; j++){
                    nums[j-1] = nums[j];
                }
                result --;
                i--;
                length--;
            }
       }
        return result;
    }
}
```
# 2. Review
虽然Java提供了内存垃圾回收器，但是在我们写程序时还是会出现内存泄漏的问题，下面举几个例子说明
##### 错误示范1
``` java
public class Stack {
    private Object[] elements;
    private int size = 0;
    private static final int DEFAULT_INITIAL_CAPACITY = 16;

    public Stack() {
        elements = new Object[DEFAULT_INITIAL_CAPACITY];
    }

    public void push(Object e) {
        ensureCapacity();
        elements[size++] = e;
    }

    public Object pop() {
        if (size == 0) throw new EmptyStackException();
        return elements[--size];
    }

    /**
     * Ensure space for at least one more element, roughly * doubling the capacity each time the array needs to grow.
     */
    private void ensureCapacity() {
        if (elements.length == size) elements = Arrays.copyOf(elements, 2 * size + 1);
    }
}
```
##### 原因
在进行出栈操作（pop)时，没有将出栈的元素删除，这会导致内存泄漏，因为这对垃圾收集器是透明的，是这个类自我管理的内存空间，修改方案如下：
``` java
public Object pop() {
    if (size == 0) throw new EmptyStackException();
    Object result = elements[--size];
    elements[size] = null; // Eliminate obsolete reference return result;
}
```
##### 错误示范2
缓存也是java内存泄漏的高发点，经常会忘记缓存已经不使用了。<br>
解决方案：<br>
场景1:当引用不被使用时，引用对象将被删除，使用WeakHashMap
场景2：当引用对象不被使用时，引用对象将被删除，使用后台进程、LinkedHashMap的removeEldestEntry方法或java.lang.ref
##### 错误示范3
监听和回调也是java内存泄漏的高发点，它们经常会不会显示的取消注册，解决方案是使用弱引用，如WeakHashMap
# 3. Tips
这次分享的技巧鸟哥的Linux私房菜中vim编辑器的使用:
![知识图](http://images.zhuhuajiancai.top/TIM%E5%9B%BE%E7%89%8720200203002420.png)
>[文章链接](http://linux.vbird.org/linux_basic/0310vi.php)

# 4. Share
分享一下耗子叔的学习技术的模板
1. 技术出现的背景
2. 该技术的优势和劣势
3. 该技术的使用场景
4. 该技术的关键组成部分和核心功能
5. 该技术的底层原理和关键实现
6. 该技术的其他实现对比
