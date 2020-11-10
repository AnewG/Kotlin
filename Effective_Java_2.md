```

You cannot use the static keyword with a class unless it is an inner class. A static inner class is a nested class which is a static member of the outer class. It can be accessed without instantiating the outer class, using other static members. Just like static members, a static nested class does not have access to the instance variables and methods of the outer class.

class MyOuter {
   static class Nested_Demo {
   }
}

成员内部类是依附外部类而存在的，也就是说，如果要创建成员内部类的对象，前提是必须存在一个外部类的对象

public class Test {
    public static void main(String[] args)  {
        //第一种方式：
        Outter outter = new Outter();
        Outter.Inner inner = outter.new Inner();  //必须通过Outter对象来创建
         
        //第二种方式：
        Outter.Inner inner1 = outter.getInnerInstance();
    }
}
 
class Outter {
    private Inner inner = null;
    public Outter() {
         
    }
     
    public Inner getInnerInstance() {
        if(inner == null)
            inner = new Inner();
        return inner;
    }
      
    class Inner {
        public Inner() {
             
        }
    }
}

Instantiating a static nested class is a bit different from instantiating an inner class. The following program shows how to use a static nested class.

public class Outer {
   static class Nested_Demo {
      public void my_method() {
         System.out.println("This is my nested class");
      }
   }
   public static void main(String args[]) {
      Outer.Nested_Demo nested = new Outer.Nested_Demo();
      nested.my_method();
   }
}

静态内部类也是定义在另一个类里面的类，只不过在类的前面多了一个关键字static。静态内部类是不需要依赖于外部类的，这点和类的静态成员属性有点类似，并且它不能使用外部类的非static成员变量或者方法，因为在没有外部类的对象的情况下，可以创建静态内部类的对象，如果允许访问外部类的非static成员就会产生矛盾，因为外部类的非static成员必须依附于具体的对象

构建器（Builder）模式

public class Person {
    private final String name ;
    private final int age;
    private final String gender;
 
    private final String education;
    private final String people;
    private final String nationality;
 
    private Person(Builder builder){
        this.name = builder.name;
        this.age = builder.age;
        this.gender = builder.gender;
        this.education = builder.gender;
        this.people = builder.people;
        this.nationality = builder.nationality;
    }
 
    public static class Builder{
        private String name;
        private int age;
        private String gender;
        private String education;
        private String people;
        private String nationality;
 
        public Builder(String name, int age, String gender){
            this.name = name;
            this.age = age;
            this.gender = gender;
        }
        public Builder education(String education){
            this.education = education;
            return this;
        }
        public Builder people(String people){
            this.people = people;
            return this;
        }
        public Builder nationality(String nationality){
            this.nationality = nationality;
            return this;
        }
        public Person build(){
            return new Person(this);
        }
    }
}
 
//Builder内部静态类是Person的静态成员(static), new Person.Builder返回Builder类的对象，所以this正常使用，最后通过build方法重新取值生成一个Person对象
Person person = new Person.Builder("A", 16, "male").education("bachelor").people("han").nationality("China").build();

Builder模式的确有它自身的不足，为了创建对象，必须先创建它的构建器。在某些十分注重性能的情况下创建构造器的开销可能是个问题。Builder模式还比重叠构造器模式还要冗长，因此它旨在有很多参数的时候才使用。

简而言之，如果类的构造器或者静态工厂中具有多个参数，设计这种类时，Builder模式就是一种不错的选择，特别是当大多数参数都是可选或者类型相同的时候。与使用重叠构造器相比，使用Builder模式的代码将更易于阅读与编写，构建器也比JavaBean更加安全。

```
