# 2.3 Abstract Class and Interface

## 1. Abstract Method

### 1.1 What is abstract method

* `Abstract method` is a method with only the method header but no method body. `Abstract method` has the name, the parameter list and the return type, so it tells what the methods is for and how to use it. But since it does not have a body, it does not provide the details of the implementation of it.  

### 1.2 How to define

* Abstract method` is a method with only keyword `abstract`, the method header and ";"

  ```java
  // Example of abstract method
  public abstract double calcArea();
  ```

  

## 2. Abstract Class

### 2.1 What is Abstract Class

* `Abstract class` is a class that may contain `abstract method`, (it can also contain normal method). On the other hand, **normal classes are not allowed to have `abstract methods`**. 

* Except can have abstract methods in the class, there is no difference between an abstract class and a regular class, both of them can have data members, static variables, and regular methods.

  

### 2.2 How to Define 

Abstract class is a class defined with keyword `abstract`. 

```java
// Example of an abstract class, this abstract class contains both abstract method and normal methods
public abstract class Shape {

    /**
     * Calculates the area of a shape
     *
     * @return the area of a shape
     */
    public abstract double calcArea();      	// abstract method, with no body

    /**
     * Calculates the perimeter of a shape
     *
     * @return the perimeter of a shape
     */
    public abstract double calcPerimeter();      // abstract method, with no body

    /**
     * Normal methods are allowed
     */
    private void print() {
        System.out.println("hello");
    }
}
```

### 2.3 When to Use Abstract Class

Usually an `Abstract class` is a superclass. By defining a superclass abstract, we can add `abstract methods` in it. In this case, all subclasses of that class will also inherit the abstract methods, and then they can **override** it in the way they want. Adding abstract methods in the superclass forces the subclass to implement those methods. You can also understand it as the superclass creates a Todo List for all the subclasses, and the subclasses have to complete the Todo List by overriding the abstract methods. (A subclass can also choose to not override the abstract method, then that class should also be defined as an abstract class)

In the previous example, the `Shape` class contains two abstract methods: `calcArea()` and `calcPerimeter()`. The shape class does not represent a specific shape, so in the class we do not know what formula to use to calculate the area or parameter. But these two abstract methods will be inherited by the subclasses, which could be a more specific shape like a rectangular or a ellipse. And they can override the methods with the body to calculate the area and perimeter.

### 2.4 Downside of Abstract Class

There is a cost of using abstract class, in short you can remember it as: **you cannot create an object of an abstract class**. Take the `Shape` class for example, since it is an abstract class with two abstract methods inside. Let's assume if Java allows us to create an object of it, `Shape s = new Shape();`, then we can call methods through that object, e.g.: `s.calcArea()`. However, this method is abstract with no method body in the `Shape` class, thus Java does not know how to execute it, and that is a serious problem for Java. Because of this, Java does not allow us to create the object first. (There is a way to create the object, but you have to override all abstract methods when you create the object).

**Notice**: You can still create a reference of an abstract class. In fact, it is very common to see that, e.g.: `Shape s = new Circle();`  , if the `Circle` is a normal class that override the abstract method inherited from the `Shape` class, then `s` is just a `Shape` type reference, the object is still `Circle` type.

## 3. Interface

### 3.1 What Is Interface

The `Interface` is very similar to the abstract class, you can also defines abstract methods and regular methods in it. Interfaces are usually be used like a **plug-in**, so whatever classes want to have those methods defined in the interface can `implement` it, then it will get all the methods in the interface, just like inheriting from a superclass. 

### 3.2 Interface VS Abstract Class

Even though they are very similar, there are some differences between interfaces and abstract classes: 

1. `Interface` is not part of a hierarchy, so we use `implements` instead of `extends` to link it with a class. Also, since an interface is not part of a hierarchy, there is no restriction of number of interfaces a class can implements (each class can only have 1 superclass).
2. Classes (even abstract classes) can have data members, however, it is not allow to have data member defined in interfaces, only static variables are allowed (final).
3. In general, interfaces allow to have 
   1. static variables (final)
   2. abstract methods
   3. default methods (normal)
4. Abstract classes allow to have
   1. data member
   2. static variables
   3. abstract methods
   4. default methods
5. Everything in an interface is `public`, (not allow to have `private`, `protected`), so if there is a variable or a method without access modifier in the interface, it is `public` instead of `default`

|                          | Regular Class | Abstract Class | Interface  |
| ------------------------ | ------------- | -------------- | ---------- |
| Defining                 | class         | class          | interface  |
| Linking with other class | extends       | extends        | implements |
| Data  Member             | Yes           | Yes            | No         |
| Static variable          | Yes           | Yes            | Yes        |
| Abstract method          | No            | Yes            | Yes        |
| Regular method           | Yes           | Yes            | Yes        |
| Creating object          | Yes           | No             | No         |


### 3.3 How to Define

Defining an Interface is similar to defining a class:

```java
// Example of an interface
public interface Drawable {
//    private String name;        // data members are not allow

    static String name = "";      // static variables are allow, and by default they are final (constant)

    /**
     * Draws the shape
     */
    void draw();         // abstract method allow, and no need for keyword "abstract"

    default void print() {       // normal methods allow, with keyword "default"
        System.out.println("hello");
    }

}
```

* Usually there are two ways to name an interface
  1. **Verb + able**: E.g.: Parkable
  2. **Noun**: E.g.: Parking

### 3.4 More Interface examples

```java
/**
 *
 * @author adinashby
 */
interface Bicycle {
    
    final static int maxNumberOfBicycles = 10;
    
    public void changeCadence(int newValue);
    
    // same as changeCadence in terms of accessibility
    void changeGear(int newValue);
    
    void speedUp(int increment);
    
    void applyBrakes(int decrement);
    
    default void printBicycleColor() {
        System.out.println("Blue");
    }
}
```
```java
public interface Printable {
    void printStates();
}
```
```java
public class MountainBicycle implements Bicycle, Printable {
    
    int cadence = 0;
    int speed = 0;
    int gear = 1; 

    @Override
    public void changeCadence(int newValue) {
       cadence = newValue;
    }

    @Override
    public void changeGear(int newValue) {
       gear = newValue;
    }

    @Override
    public void speedUp(int increment) {
        speed += increment;
    }

    @Override
    public void applyBrakes(int decrement) {
        speed -= decrement;
    }
    
    @Override
    public void printStates() {
        System.out.println("Cadence: " + cadence + "\nSpeed: " + speed + "\nGear: " + gear 
                + "\nMaxNumberOfBicycles: " + maxNumberOfBicycles);
        
        printBicycleColor();
    }
    
}
```
```java
public class MyProject {
    public static void main(String[] args) {
         MountainBicycle myBicycle = new MountainBicycle();
         
         myBicycle.speedUp(5);
         myBicycle.changeGear(6);
         
         myBicycle.printStates();
    }
}
```
