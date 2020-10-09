# Java

```

[1]Java程序设计语言 [2]各种平台上的Java虚拟机(JVM) [3]JavaAPI类库 [4]一系列辅助工具

1+2+3+4 = JDK（Java Development Kit）：即Java程序开发包，是支撑Java程序开发的最小环境。
2+3 = JRE（Java Runtime Environment）：即Java运行时环境，是支撑Java程序运行的最小环境。

-------------

Java SE（Java Platform，Standard Edition）
其以前被称为J2SE。标准版主要用来开发传统C/S架构的软件。通俗地讲，即开发桌面应用程序。

Java EE（Java Platform，Enterprise Edition）
其以前被称为J2EE。企业版是开发和部署可移植、健壮、可伸缩、安全的服务端Java应用，典型的就是企业Web服务。

早期SSH (Struts+Spring+Hibernate，已过时)
现今SSM (Spring+SpringMVC+MyBatis) MyBatis是DB层,避免了几乎所有JDBC代码和手动设置参数等,简化CRUD流程
更加先进的 Spring Boot[Spring脚手架], Spring Cloud

Java ME（Java Platform，Micro Edition）
微型版是为在移动、嵌入式设备上运行的Java应用提供的平台环境。

项目管理：https://gradle.org/maven-vs-gradle/

-------------

'A'是编码值为65所对应的字符常量。它与"A"不同，"A"是包含一个字符A的字符串。

Unicode转义序列会在解析代码之前得到处理。例如，"\u0022+\u0022"并不是一个由引号（U+0022）包围加号构成的字符串。实际上，\u0022会在解析之前转换为"，这会得到""+""，也就是一个空串。

要想对文件进行读取，就需要一个用File对象构造一个Scanner对象，如下所示：
Scanner in = new Scanner(Paths.get("myfile.txt"), "UTF-8");
如果文件名中包含反斜杠符号，就要记住在每个反斜杠之前再加一个额外的反斜杠：“c：\\mydirectory\\myfile.txt”。

不能在嵌套的两个块中声明同名的变量

一旦创建了数组，就不能再改变它的大小（尽管可以改变每一个数组元素）。如果经常需要在运行过程中扩展数组的大小，就应该使用另一种数据结构——数组列表（arraylist）

方法可以访问所调用对象的私有数据。一个方法可以访问所属类的所有对象的私有数据。访问控制是基于类而不是基于对象

总是采用按值调用。也就是说，方法得到的是所有参数值的一个拷贝。对象引用也属于复制

可以调用方法对域进行初始化
class A{
	private static int nextId;
	private int id = assignId();
	private static int assignId(){
		int r = nextId;
		nextId++;
		return r;
	}
}

调用另一个构造器
public A(double s){
	this(nextId, s); // A(String, double)构造器
}

设置类路径相当于额外指定类文件搜索基准目录，类似于php的set_include_path

Java不支持多继承。Java中多继承功能的实现方式为接口

返回类型不是签名的一部分，因此，在覆盖父类方法时，一定要保证返回类型的兼容性。允许子类将覆盖方法的返回类型定义为原返回类型的子类型

在覆盖一个方法的时候，子类方法不能低于超类方法的可见性。特别是，如果超类方法是public，子类方法一定要声明为public

对于final域来说，构造对象之后就不允许改变它们的值了。不过，如果将一个类声明为final，只有其中的方法自动地成为final，而不包括域

为了避免发生未覆盖到或其他类型错误，可以使用@Override对覆盖超类的方法进行标记，比如方法并没有覆盖超类中的任何方法将会报错

int不是类，但int.class是一个Class类型的对象。(反射相关)

抽象类与接口的区别，每个类只能扩展于一个抽象类，但每个类可以实现多个接口[类多重继承]

如果先在一个接口中将一个方法定义为默认方法，然后又在超类或另一个接口中定义了同样的方法，将有以下规则
(1）超类优先。如果超类提供了一个具体方法，同名而且有相同参数类型的默认方法会被忽略。
(2）接口冲突。如果一个超接口提供了一个默认方法，另一个接口提供了一个同名而且参数类型（不论是否是默认参数）相同的方法，必须覆盖这个方法来解决冲突。

lambda表达式中捕获的变量(闭包)必须实际上是最终变量（effectivelyfinal）。实际上的最终变量是指，这个变量初始化之后就不会再为它赋新值。

函数式接口：https://www.runoob.com/java/java8-functional-interfaces.html

内部类（innerclass）是定义在另一个类中的类。
  为什么需要使用内部类呢？其主要原因有以下三点：
    内部类方法可以访问该类定义所在的作用域中的数据，包括私有的数据。
    内部类可以对同一个包中的其他类隐藏起来。
    当想要定义一个回调函数且不想编写大量代码时，使用匿名（anonymous）内部类比较便捷。

Link类位于LinkedList类的私有部分，因此，Link对其他的代码均不可见。
鉴于此情况，可以将Link的数据域设计为公有的，它仍然是安全的。这些数据域只能被LinkedList类（具有访问这些数据域的合理需要）中的方法访问，而不会暴露给其他的代码。
在Java中，只有内部类能够实现这样的控制。

异常层次结构：Throwable --> [Error + Exception]--> IOException, RuntimeException... 

断言机制允许在测试期间向代码中插入一些检查语句。当代码发布时，这些插入的检测语句将会被自动地移走

---------------

对类型作出限定(bound)
public static <T extends ....接口> ...
public static <T extends ....接口 & ...接口2> ...

比如，Base 是 Sub 的父类，它们之间是继承关系，所以 Sub 的实例可以给一个 Base 引用赋值，但是

List<Sub> lsub = new ArrayList<>();
List<Base> lbase = lsub;

编译器不会让它通过的。Sub 是 Base 的子类，不代表 List<Sub>和 List<Base>有继承关系。
若希望泛型能够处理某一范围内的数据类型，比如某个类和它的子类，对此 Java 引入了通配符这个概念。
所以，通配符的出现是为了指定泛型中的类型范围。

通配符有 3 种形式。
<?> 被称作无限定的通配符
<? extends T> 被称作有上限的通配符
<? super T> 被称作有下限的通配符

泛型信息只存在于代码编译阶段，在进入 JVM 之前，与泛型相关的信息会被擦除掉，专业术语叫做类型擦除
类型擦除，是泛型能够与之前的 java 版本代码兼容共存的原因

在泛型类被类型擦除的时候，之前泛型类中的类型参数部分如果没有指定上限，如 <T>则会被转译成普通的 Object 类型
如果指定了上限如 <T extends String>则类型参数就被替换成类型上限。
若类型变量有多个限定，那么原始类型就用第一个边界的类型变量来替换。而编译器在必要的时要向第一个边界类型插入强制类型转换。
为了提高效率，应该将标签（tagging）接口（即没有方法的接口）放在边界限定列表的末尾。

所以可以利用反射调用方法来绕过编译器限制

在应用泛型类的时候，如果返回值也是泛型，那么返回的将是Object
但是很显然，我们在使用泛型的过程中，并没有要显示的进行类型转换，比如我们不需要这样 String a=(String) super.method("hahaha")
而是直接 String a= super.method("hahaha"); 就可以了。为什么呢？

是因为，为了返回实现类型的自动匹配，java编译器会在“类型擦除”的基础上在进行“转换插入”操作。
每当使用泛型的返回值时，编译器会制动插入类型转换，所以原始代码是 String a= super.method("hahaha"); 
编译之后，虚拟机看到的却是 String a= (String)super.method("hahaha"); 类型转换被“插入”了。

因为类型擦除后，原有的泛型方法的泛型参数都被替换成了Object，因此无法实现方法覆盖，但实际应用中，肯定需要实现方法覆盖从而达到多态的目的。
为了实现对method方法的覆盖，编译器在进行编译时，自动插入了一个桥接方法
public Object mehoed(Object arv){
    return method((String) arv);
}
桥接方法的方法签名和返回值和父类的泛型方法 public Object mehoed(Object arv) 一致，因此可以覆盖父类的method方法，实现了多态。
通过桥接方法，还实现了对用户定义的method方法的调用，在程序员看来，就好像 public String mehoed(String arv) 成功覆盖了 public Object mehoed(Object arv) 一样。

---------------

泛型类或者泛型方法中，不接受 8 种基本数据类型。
所以，你没有办法进行这样的编码。

List<int> li = new ArrayList<>();
List<boolean> li = new ArrayList<>();

需要使用它们对应的包装类。

List<Integer> li = new ArrayList<>();
List<Boolean> li1 = new ArrayList<>();

---------------

泛型的限制：

正因为java是以这种比较奇怪的方式实现了泛型，因此一切new T（..）或者new T[]其实都会是new Object，没有任何意义，所以java干脆在编译阶段就禁止了这种语法
也就是说，泛型只能传入，不能产生。

上面说泛型在编译阶段就被“擦除”了，其实也不完全对，利用反射，仍然可以获取泛型信息，比如泛型参数、泛型限制、通配符信息等都可以获取到
说明在java的字节码（即.class文件）中，泛型信息仍然存在。
因此，更准确的说，是泛型经过类加载器加载到虚拟机之后，泛型比擦除了，但是泛型的信息仍然存在字节码中，并且可以通过反射获取到。


1.模糊性错误

声明了两个泛型类参数。在类中根据不同的类型参数重载show方法。

public class User<K, V> {
    public void show(K k) {} // error：'show(K)' clashes with 'show(V)'; both methods have same erasure
    public void show(V t) {}
}

复制代码由于泛型擦除，二者本质上都是Obejct类型。

换一个方式即可：

public class User<K, V> {
    public void show(String k) {} // show(String)
    public void show(V t) {}  // show(Object)
}

2.不能实例化类型参数

编译器也不知道该创建那种类型的对象

public class User<K, V> {
    private K key = new K(); // 报错：Type parameter 'K' cannot be instantiated directly
}

3.对静态成员的限制

静态方法无法访问类上定义的泛型
如果静态方法操作的类型不确定，必须要将泛型定义在方法上。
如果静态方法要使用泛型的话，必须将静态方法定义成泛型方法。

public class User<T> {
    private static T t; //错误
    public static T getT() {} //错误
    public static <K> void test(K k) {} //正确
}

4.对泛型数组的限制

不能实例化元素类型为类型参数的数组，但是可以将数组指向类型兼容的数组的引用

public class User<T> {

    private T[] values;

    public User(T[] values) {
        this.values = new T[5]; //错误，不能实例化元素类型为类型参数的数组
        this.values = values; //正确，可以将values 指向类型兼容的数组的引用
    }
}

5.对泛型异常的限制

泛型类不能扩展 Throwable，意味着不能创建泛型异常类
https://stackoverflow.com/questions/501277/why-doesnt-java-allow-generic-subclasses-of-throwable

---------------

Apache HTTP Server和Nginx本身不支持生成动态页面，但它们可以通过其他模块来支持（例如通过Shell、PHP、Python脚本程序来动态生成内容）
如果想要使用Java程序来动态生成资源内容，使用这一类HTTP服务器很难做到。虽然nginx也可以通过模块开发来提供对应功能

Java Servlet技术以及衍生的技术可以让Java程序也具有处理HTTP请求并且返回内容（由程序动态控制）的能力
Tomcat正是支持运行Servlet/JSP应用程序的容器（Container），对应同级别的有jboss,jetty等
Tomcat运行在JVM之上，它和HTTP服务器一样，绑定IP地址并监听TCP端口，同时还包含以下指责：
1.管理Servlet程序的生命周期
2.将URL映射到指定的Servlet进行处理
3.与Servlet程序合作处理HTTP请求

虽然Tomcat也可以认为是HTTP服务器单独提供服务（通常用在内网和不需要流控等小型服务的场景），但通常它仍然会和Nginx配合在一起使用

1.动静态资源分离——运用Nginx的反向代理功能分发请求：所有动态资源的请求交给Tomcat，而静态资源的请求（例如图片、视频、CSS、JavaScript文件等）则直接由Nginx返回到浏览器，这样能大大减轻Tomcat的压力。
2.负载均衡，当业务压力增大时，可能一个Tomcat的实例不足以处理，那么这时可以启动多个Tomcat实例进行水平扩展，而Nginx的负载均衡功能可以把请求通过算法分发到各个不同的实例进行处理

---------------

当一个共享变量被volatile修饰时，它会保证修改的值会立即被更新到主存，当有其他线程需要读取时，它会去内存中读取新值。

而普通的共享变量不能保证可见性，因为普通共享变量被修改之后，什么时候被写入主存是不确定的，当其他线程去读取时，此时内存中可能还是原来的旧值，因此无法保证可见性。

另外，通过synchronized和Lock也能够保证可见性，synchronized和Lock能保证同一时刻只有一个线程获取锁然后执行同步代码，并且在释放锁之前会将对变量的修改刷新到主存当中。因此可以保证可见性。

但volatile并不能保证对其进行的操作是原子性的，只是保证了读取的可见性

===================================================

在使用某些驱动程序时，使用保存点（savepoint）可以更细粒度地控制回滚操作

假设有一个程序需要执行许多INSERT语句，以便将数据填入数据库表中，此时可以使用批量更新的方法来提高程序性能。在使用批量更新（batchupdate）时，一个语句序列作为一批操作将同时被收集和提交


```












## Structure of a java class

```
/*
  orgType  is the organization type, such as com, org, or net.
  orgName  is the name of the organization's domain, such as makotojava, oracle, or ibm.
  appName  is the name of the application, abbreviated.
  compName is the name of the component.
*/
package orgType.orgName.appName.compName;

import com.makotojava.*;

accessSpecifier class ClassName extends Xxx {

  // private String name;
  accessSpecifier static final dataType variableName [= initialValue];

  accessSpecifier ClassName([argumentList]) {
    constructorStatement(s)
    System.out.println("Telling you all about it:");
  }
  
  /*
    public String getName() { return name; }
    public void setName(String value) { name = value; }
  */
  accessSpecifier returnType methodName ([argumentList]) {
    methodStatement(s)
  }
  
  // type
  public void typeMethod(){
    // boxing
    int value = 238;
    Integer boxedValue = Integer.valueOf(value);
    // unbox
    Integer boxedValue = Integer.valueOf(238);
    int intValue = boxedValue.intValue();
    // auto
    int intValue = 238;
    Integer boxedValue = intValue;
    intValue = boxedValue;
  }
  
  // scope
  private String someClassVariable;
  public void someMethod(String someParameter) {
    String someLocalVariable = "Hello";
    if (true) {
      String someOtherLocalVariable = "Howdy";
    }
    someClassVariable = someParameter;          // legal
    someLocalVariable = someClassVariable;      // also legal
    someOtherLocalVariable = someLocalVariable; // Variable out of scope!
  }
  
  // collections
  // array
  public void someOtherMethod() {
    someLocalVariable = "Hello there";// That variable is out of scope!
    int[] integers = new int[5];
    int[] integers2 = new int[] { 1, 2, 3, 4, 5 };
    int[] integers3 = { 1, 2, 3, 4, 5 };
    int[] integers4 = new int[5];
    for (int aa = 0; aa < integers.length; aa++) {
      integers4[aa] = aa+1;
    }
    for (int i : integers) {
      // i
    }
  }
  // list
  public void listMethod(){
    List<Integer> listOfIntegers = new ArrayList<>();
    listOfIntegers.add(Integer.valueOf(238));
    listOfIntegers.size()
    listOfIntegers.get(0)
  }
  // sets
  public void setsMethod(){
    Set<Integer> setOfIntegers = new HashSet<Integer>();
    setOfIntegers.add(Integer.valueOf(10));
  }
  // Maps
  @Override
  public void mapsMethod(){
    Map<String, Integer> mapOfIntegers = new HashMap<>();
    mapOfIntegers.put("1", Integer.valueOf(1));
    mapOfIntegers.get("1")
  }
  
  // try-with-resource
  public void exceptionTestTryWithResources() {
    Logger l = Logger.getLogger(Employee.class.getName());
    File file = new File("file.txt");
    try (BufferedReader bufferedReader = new BufferedReader(new FileReader(file))) {
      String line = bufferedReader.readLine();
      while (line != null) {
        // Read the file
      }
    } catch (Exception e) {
      l.severe(e.getMessage());
    }
  }
}
```

## abstract

```
public abstract class Employee
{
   private String name;
   private String address;
   private int number;
   
   public abstract double computePay();
}
```

## interface

```
public interface InterfaceName {
  returnType methodName(argumentList);
}
public class Manager extends Employee implements BonusEligible, StockOptionRecipient {
  // And so on
}
```

## nested class

```
public class Manager extends Employee {
  public Manager() {
  }
  . . .
  public class DirectReports {
  . . .
  }
}

// Meanwhile, in another method somewhere...
public static void main(String[] args) {
  Manager manager = new Manager();
  Manager.DirectReports dr = manager.new DirectReports();
}

ref: https://www.jianshu.com/p/b7f9c806b3aa
```

## Overload

```
public void printAudit(StringBuilder buffer) {
   buffer.append("Name=");
}
 
public void printAudit(Logger l) {
   StringBuilder sb = new StringBuilder();
   printAudit(sb);
   l.info(sb.toString());
}
```

## enum

```
public enum Gender {
  MALE("male"),
  FEMALE("female"),
  OTHER("other");
 
  private String displayName;
  private Gender(String displayName) {
    this.displayName = displayName;
  }
 
  public String getDisplayName() {
    return this.displayName;
  }
}
```

## JAR

```
src/...
lib/xxx.jar (Add to Build Path)
```

## Generics

```
ArrayList is Generics:
  ArrayList<String> strList = new ArrayList<String>();  
  ArrayList<Integer> intList = new ArrayList<Integer>();  
  ArrayList<Double> doubleList = new ArrayList<Double>();  
  
-------------------------

class Point<T>{   
    private T x ;        
    private T y ;        
    public void setX(T x){
        this.x = x ;  
    }  
    public void setY(T y){  
        this.y = y ;  
    }  
    public T getX(){
        return this.x ;  
    }  
    public T getY(){  
        return this.y ;  
    }  
};  
Point<Integer> p = new Point<Integer>() ;   
p.setX(new Integer(100)) ;   
System.out.println(p.getX());    

Point<Float> p = new Point<Float>() ;   
p.setX(new Float(100.12f)) ;   
System.out.println(p.getX());  

-------------------------

class MorePoint<T,U> {  
    private T x;  
    private T y;         
    private U name;  
    public void setX(T x) {  
        this.x = x;  
    }  
    public T getX() {  
        return this.x;  
    }  
    public void setName(U name){  
        this.name = name;  
    }  
    public U getName() {  
        return this.name;  
    }  
}
MorePoint<Integer,String> morePoint = new MorePoint<Integer, String>();  
morePoint.setName("harvic");  
Log.d(TAG, "morPont.getName:" + morePoint.getName());  

-------------------------

interface Info<T>{    
    public T getVar();  
    public void setVar(T x);  
}    

http://blog.csdn.net/qq_27093465/article/details/73229016
```
