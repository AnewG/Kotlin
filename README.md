# Java

sth about java

## Java Tutorials

[Basic](https://learnxinyminutes.com/docs/zh-cn/java-cn/)

[Introduction to Java programming, Part 1](https://www.ibm.com/developerworks/java/tutorials/j-introtojava1/index.html)

[Introduction to Java programming, Part 2](https://www.ibm.com/developerworks/java/tutorials/j-introtojava2/index.html)

[Android studio run standard Java projects](https://stackoverflow.com/questions/16626810/can-android-studio-be-used-to-run-standard-java-projects)

## Structure of a java class

```
package orgType.orgName.appName.compName;
/*
  orgType  is the organization type, such as com, org, or net.
  orgName  is the name of the organization's domain, such as makotojava, oracle, or ibm.
  appName  is the name of the application, abbreviated.
  compName is the name of the component.
*/

import com.makotojava.*;

accessSpecifier class ClassName {

  accessSpecifier dataType variableName [= initialValue];
  /*
    private String name;
    private int age;
  */
  
  accessSpecifier ClassName([argumentList]) {
    constructorStatement(s)
  }
  
  accessSpecifier returnType methodName ([argumentList]) {
    methodStatement(s)
  }
  /*
  public String getName() { return name; }
  public void setName(String value) { name = value; }
  */
  
  private String someClassVariable;
  public void someMethod(String someParameter) {
    String someLocalVariable = "Hello";
 
    if (true) {
      String someOtherLocalVariable = "Howdy";
    }
    someClassVariable = someParameter; // legal
    someLocalVariable = someClassVariable; // also legal
    someOtherLocalVariable = someLocalVariable;// Variable out of scope!
  }
  public void someOtherMethod() {
    someLocalVariable = "Hello there";// That variable is out of scope!
    int[] integers = new int[5];
    int[] integers2 = new int[] { 1, 2, 3, 4, 5 };
    int[] integers3 = { 1, 2, 3, 4, 5 };
    int[] integers4 = new int[5];
    for (int aa = 0; aa < integers.length; aa++) {
      integers4[aa] = aa+1;
    }
  }
  
  // This is a comment
  /* This is a comment too */
  /* This is a
     multiline
     comment */
}
```
