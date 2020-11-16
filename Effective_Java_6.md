```

static boolean isRomanNumeral(String s) {
    return s.matches("^(?=.)M*(C[MD]|D?C{0,3})"
            + "(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");
}

这个实现的问题在于它依赖于 String.matches 方法。 虽然 String.matches 是检查字符串是否与正则表达式匹配的最简单方法，但它不适合在性能临界的情况下重复使用。 问题是它在内部为正则表达式创建一个 Pattern 实例，并且只使用它一次，之后它就有资格进行垃圾收集。 创建 Pattern 实例是昂贵的，因为它需要将正则表达式编译成有限状态机（finite state machine）

// Reusing expensive object for improved performance
public class RomanNumerals {
    private static final Pattern ROMAN = Pattern.compile(
            "^(?=.)M*(C[MD]|D?C{0,3})"
            + "(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");

    static boolean isRomanNumeral(String s) {
        return ROMAN.matcher(s).matches();
    }
}

不要错误地认为本条目所介绍的内容暗示着“创建对象的代价非常昂贵，我 应该要
尽可能地避免创建对象” 相反，由于小对象的构造器只做很少量的显式工作，所以小对象
的创建和回收动作是非常廉价的，特别是在现代的 JVM 实现上更是如此 通过创建附加的
对象，提升程序的清晰性、简洁性和功能性，这通常是件好事

反之，通过维护自己的对象池（ object pool ）来避免创建对象并不是一种好的做法，除
非池中的对象是非常重量级的 正确使用对象池的典型对象示例就是数据库连接池 建立数
据库连接的代价是非常昂贵的，因此重用这些对象非常有意义 而且，数据库的许可可能限
制你只能使用一定数量的连接 但是，一般而言，维护自己的对象池必定会把代码弄得很
乱，同时增加内存占用（ footprint ），并且还会损害性能 现代的 JVM 实现具有高度优化的
垃圾回收器，其性能很容易就会超过轻量级对象池的性能

```
