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
  
  // This is a comment
  /* This is a comment too */
  /* This is a
     multiline
     comment */
}
```
