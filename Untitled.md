1) Below class ABC doesn’t have even a single abstract method, but it has been declared as abstract. Is it correct? 
```java
abstract class ABC {
	void firstMethod() { 
		System.out.println("First Method"); 
	} 
	void secondMethod() { 
		System.out.println("Second Method"); 
	} 
}
```

**Answer**:
Yes, it can be done, since we can maintain any level of abstraction in abstract classes (0-100%)

2) Why the below class is showing compilation error?
```java
abstract class AbstractClass 
{ 
	abstract void abstractMethod() 
	{ 
		System.out.println("First Method"); 
	} 
} 
```

**Answer**:
Abstract methods are expected not to have a definition closure, but the abstract function `abstractMethod()` has a definition.

3) Which class is instantiable
```java
abstract class A 
{ 
} 
class B extends A 
{ 
}
```

**Answer**:
Class A is an abstract class, so it cannot be instantiated with `new`
Class B is a concrete class which inherits A. Since its still a concrete, it can be done.

4) Below code snippet is showing compilation error? Can you suggest the corrections?
```java
abstract class A 
{ 
	abstract int add(int a, int b); 
} 
class B extends A 
{ 
}
```

**Answer**
Class B has inherited abstract method add from Class A (abstract), but does not have its definition, which ultimately results in an error.

5) Is the following program written correctly? If yes, what value “result” variable will hold if you run the program? 
```java
abstract class Calculate 
{ 
	abstract int add(int a, int b); 
} 
public class MainClass 
{ 
	public static void main(String[] args) 
	{ 
		int result = new Calculate() 
		{    
			@Override 
			int add(int a, int b) 
			{ 
				return a+b; 
			} 
		}.add(11010, 022011); 
	} 
} 
```

**Answer**
This program will run correctly.
- line 9 represents an **Anonymous Inner Class** which inherits from the Calculate(), without any object identifier. 
- **Lambda expressions** (anonymous objects)
```java
(params) -> {definition}
```
- line 16 adds an integer and an octal
  second integer starts with `0`, indicating an Octal representation
	(0b - binary, 0 - Octal, 0x - hexadecimal)

Hence, the output will be 
```sh
20235
```

6) Can we write explicit constructors in an abstract class?
**Answer:**
We can explicitly define concrete constructors in an abstract class, similar to regular classes, which does not raise any error.

Example: 
```java
abstract class A {
    A(){
        System.out.println("Hello from A");
    }
    abstract void gg(int b1);
}

class B extends A {
    void gg(int x){
    }
}

class One {
    public static void main (String args[]){
        A a1 = new B();
    }
}
```

##### Note:
```java
abstract class A {
    A(int a1, int a2){
        System.out.println(a1+a2);
    }
    abstract void gg(int b1);
}

class B extends A {
    B(){
        super(5,10); //super is needed to call parameterized super constructors
    }
    void gg(int x){
        x+=2;
    }
}

class One {
    public static void main (String args[]){
        B a1 = new B();
    }
}
```

7) Can you identify the error in the below code? 
```java
abstract class AbstractClass 
{ 
	private abstract int abstractMethod(); 
}
```

**Answer**
abstract and private modifiers cannot be declared together. for abstraction to work, the method must be public for the subclasses to overwrite it. Works for protected too

> Note: Abstract classes wont support `static` too

8) Can we declare protected methods in an interface?
**Answer**
No
Interfaces are meant to provide a structure to classes outside **(implementing)** and not **extending**. the methods are public by default, and private methods can be declared as helper functions, but **protected** modifier affects only the **Interface inheritance** (sub interface extending another interface) which is meaningless when applying to class methods.

9) What will be the output of the following program? 
```java
abstract class A 
{ 
    abstract void firstMethod(); 
      
    void secondMethod() 
    { 
        System.out.println("SECOND"); 
          
        firstMethod(); 
    } 
} 
  
abstract class B extends A 
{ 
    @Override 
    void firstMethod() 
    { 
        System.out.println("FIRST"); 
          
        thirdMethod(); 
    } 
      
    abstract void thirdMethod(); 
} 
  
class C extends B 
{ 
    @Override 
    void thirdMethod() 
    { 
        System.out.println("THIRD"); 
    } 
} 
  
public class MainClass 
{ 
    public static void main(String[] args) 
    { 
        C c = new C(); 
          
        c.firstMethod(); 
          
        c.secondMethod(); 
          
        c.thirdMethod(); 
    } 
} 
```

**Output:**
```sh
FIRST
SECOND
THIRD
```

10) What will be the output of the below program?
```java
abstract class X 
{ 
    public X() 
    { 
        System.out.println("ONE"); 
    } 
      
    abstract void abstractMethod(); 
} 
  
class Y extends X 
{ 
    public Y()  
    { 
        System.out.println("TWO"); 
    } 
      
    @Override 
    void abstractMethod() 
    { 
        System.out.println("THREE"); 
    } 
} 
  
public class MainClass 
{ 
    public static void main(String[] args) 
    { 
        X x = new Y(); 
          
        x.abstractMethod(); 
    } 
}
```

output
```sh
ONE
TWO
THREE
```

11) Can we declare abstract methods as static?
**Answer**
No
static modifier makes a method 's definition available even if it is not overwritten in its objects (instances). abstract modifier declares that the method wont have a definition. They are contradictory.

12) Is the below program written correctly? If yes, what will be the output? 
```java
abstract class A 
{ 
	{ 
		System.out.println("AAA"); 
	} 
} 
abstract class B extends A 
{ 
	{
		System.out.println("BBB"); 
	} 
}  
class C extends B 
{ 
	{
		System.out.println("CCC");
	} 
} 
 
public class MainClass 
{ 
	public static void main(String[] args) 
	{ 
		C c = new C(); 
	} 
}
```

**Output**
```sh
AAA
BBB
CCC
```

**13) What will be the output of the following program?**

```java
abstract class A {

abstract int firstMethod(int i);

abstract int secondMethod(int i);

int thirdMethod(int i) {

return secondMethod(++i);

}

}

abstract class B extends A {

@Override

int secondMethod(int i) {

return firstMethod(++i);

}

}

class C extends B {

@Override

int firstMethod(int i) {

return ++i;

}

}

public class MainClass {

public static void main(String[] args) {

C c = new C();

System.out.println(c.thirdMethod(121121));

}

}
```
**_Solution:_**

121124

**14) Can we keep static initialization blocks inside an abstract class?**

Yes, we can have static initialization blocks inside an abstract class in Java. Static initialization blocks are executed when the class is first loaded into memory, regardless of whether the class is abstract or concrete.

**_Example:_**

```java
abstract class Example {

static {

System.out.println("Static block in abstract class");

}

}
```

**15) Is the below program written correctly? If yes, what will be the output?**

```java
abstract class XYZ {

{System.out.println(1);}

public XYZ() {

System.out.println(2);

abstractMethod();

}

abstract void abstractMethod();

}

class PQR extends XYZ {

{ System.out.println(3);}

public PQR() {

System.out.println(4);

}

@Override

void abstractMethod() {

System.out.println(5);

}

}

public class MainClass {

public static void main(String[] args) {

PQR pqr = new PQR();

}

}
```

**_Solution:_**

1

2

5

3

4

**16) Can you identify the error in the below code?**

```java
class X {

public X() {

System.out.println("Constructor One");

}

abstract X(int i) {

System.out.println("Constructor Two");

}

}
```

**_Solution:_**

The constructors cannot be abstract in Java.

**17) Abstract methods can be declared as final. True or False?**

False, Abstract Methods cannot be declared as final. Because it contradicts the purpose as method cannot be overridden.

**18) Is the below code written correctly?**

```java
class X {

abstract class Y

{

class Z

{

}

}

}
```

**_Solution:_**

No, an abstract class cannot be written inside a non-abstract class without being properly declared. Also, there is a syntax error in the nested class declaration.

**19) What will be the output of the following program?**

```javab
[]
class ClassOne {

int methodOne(int i, int j) {

return i++ + ++j - ++i - j++;

}

}

abstract class ClassTwo extends ClassOne {

abstract int methodOne(int i, int j, int k);

@Override

int methodOne(int i, int j) {

return methodOne(i, j, i+j);

}

}

class ClassThree extends ClassTwo {

@Override

int methodOne(int i, int j, int k) {

return --i - j-- + ++k - i++ + ++j - k--;

}

}

public class MainClass{

public static void main(String[] args) {

ClassOne one = new ClassOne();

ClassThree three = new ClassThree();

System.out.println(three.methodOne(one.methodOne(10101, 20202), one.methodOne(20202, 10101)));

}

}
```

**_Solution:_**

0