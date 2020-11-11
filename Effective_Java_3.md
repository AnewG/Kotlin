```

利用枚举类型实现单例-天然的防止反射和反序列化调用

------------------------

第一种实现单例的方式：公有静态类是个final域

public class Elvis {

  public static final Elvis INSTANCE = new Elvis(); //公有静态final域 Elvis.INSTANCE

  //构造器保持为私有，导出公有静态成员，客户端可以访问该类的唯一实例
  private Elvis(){
    //...
  }
}

问题：享有权限的客户端可以借助 AccessiableObject.setAccessible 方法，通过反射机制调用私有构造器。
如果需要抵御这种攻击，可以修改构造器，代码里面做个检测判断，在被要求创建第二个实例时抛出异常。还有序列号问题

-------------

第二种实现单例的方式：公有成员是个静态工厂方法

public class Elvis2 {
  // 私有final成员
  private static final Elvis2 INSTANCE = new Elvis2();

  // 静态方法公有成员
  public static Elvis2 getInstance(){
    return INSTANCE;
  }

  //构造器保持为私有，导出公有静态成员，客户端可以访问该类的唯一实例
  private Elvis2(){
    // 防止反射获取多个对象的漏洞
    if (null != Elvis2.INSTANCE) {
        throw new RuntimeException("it is a Singleton");
    }
  }

  // readResolve method to preserve singleton property, 防止序列化问题
  private Object readObject(){
    // Return the one true Elvis and let the garbage collector take care of the Elvis impersonator
    return INSTANCE;
  }
}

优点：在不改变API的前提下，可以改变此类是否应该为Singleton。比如改为每个调用该方法的线程返回一个唯一的实例
问题：同上

-------------

第三种实现单例的方式：包含单个元素的枚举类型

public class SingletonCase6 {
  enum SingletonEnum {
    //创建一个枚举对象，该对象天生为单例
    INSTANCE; //固定
/*
因为获得实例只能通过SingletonEnum.INSTANCE,下面的方式是不可以的
SingletonEnum a = new SingletonEnum(); //compile error
*/
    private SingletonCase6 singleton;

    //私有化枚举的构造函数
    private SingletonEnum() {
      System.out.println("-----1 init constructor-----");
      singleton = new SingletonCase6();
    }

    public SingletonCase6 getSingleton() {
      System.out.println("-----2 return singleton-----");
      return singleton;
    }
  }

  private SingletonCase6() {
  }

  public static SingletonCase6 getInstance(){
    System.out.println("-----3 getInstance -----");
    return SingletonEnum.INSTANCE.getSingleton();
  }

  public static void main(String[] args) {
    getInstance();
  }
}

这种方法在功能上跟公有域方法相近，但它更加简洁，无偿的提供了序列化机制，绝对防止多次实例化，即使是面对复杂的序列化或者反射攻击的时候
单例模式实际上有5种（懒汉模式/饿汉模式/双锁检测模式/内部类/枚举类）

```
