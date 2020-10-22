```

考虑用静态工厂方法代替构造器

创建对象的方法：
1. 使用类的共有构造器
2. 使用类的静态方法返回一个实例

```

```

// 定义两个类
class PersonA {
    public PersonA() {}
    
    // 调用该函数时必须先实例化PersonA对象
    public void test() {
        System.out.println("just test in PersonA \n")
    }
}

class PersonB {
    public PersonB() {}
    // 静态工厂生产方法
    public static PersonB newInstance() {
        return new PersonB();
    }
    // 调用该函数不必先实例化PersonB对象，可以通过PersonB.test()直接调用
    public static void test() {
        System.out.println("just for test in PersonB \n");
    }
}

// 实例化两个对象
PersonA pA = new PersonA();
PersonB pB = PersonB.newInstance();

```

```

静态方法的名字由我们自己命名，而构造方法必须与类同名
构造方法每次调用都会创建一个对象，而静态工厂方法每次调用的时候就不会创建一个新的对象，这对于一个频繁创建对象的程序来说，可以极大的提高性能，单例模式就是这样实现的

```

```

// 单例模式
class PersonC {
    // 1.声明一个静态成员pC
    private static PersonC pC;
    // 2.私有化构造函数
    private PersonC() {}
    // 3.通过静态函数获取一个该类的实例
    public static PersonC newInstance() {
        if (pC == null) {
            return new PersonC();
        }
    }
}

```

```

静态工厂方法创建对象的缺点
若一个类只能通过静态工厂方法获取实例，那么该类的构造函数就不能是共有的或受保护的，那么该类就不会有子类，即该类不能被继承。单例模式就必须要私有化构造函数
静态工厂方法和其他静态方法一样，都是函数，所以在区分时最好使用一些惯用名称，如valueOf、getInstance等等

```
