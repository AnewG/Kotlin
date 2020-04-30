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
