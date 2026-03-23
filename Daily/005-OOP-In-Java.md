# Today i have learning about oops(Object-Oriented Programming) :

----

## The main 4 pillars of oops:
### 1) Encapsulation :
### 2) Inheritance :
### 3) Polymorphism :
### 4) Abstraction :

----

## 1) Encapsulation :
* Encapsulation is an OOP concept that wraps data and methods together and protects the data from direct access.
* In simple words:
Encapsulation means data hiding + controlled access.
* Encapsulation mens sensitive data hide no change this data because data is private 

### Example: Bank Account (Encapsulation)

This example demonstrates encapsulation by:
- Declaring data as **private**
- Accessing data using **public methods**
- Applying validation rules before changing data

### BankAccount Class

```java
class BankAccount {

    private double balance;   // data is hidden

    public BankAccount(double totalBalance) {
        if (totalBalance >= 0) {
            this.balance = totalBalance;
        } else {
            this.balance = 0;
        }
    }

    public void deposit(double money) {
        if (money > 0) {
            balance += money;
            System.out.println("Money deposited: " + money);
        } else {
            System.out.println("Invalid deposit amount");
        }
    }

    public void withdraw(double money) {
        if (money > 0 && money <= balance) {
            balance -= money;
            System.out.println("Money withdrawn: " + money);
        } else {
            System.out.println("Withdrawal not allowed");
        }
    }

    public double getBalance() {
        return balance;
    }
}
```
----
## 2) Inheritance :
* Inheritance is a mechanism where one class acquires the attributes (variables) and methods (functions) of another class.
* In this concept:
    * Superclass (Parent Class) → base class
    * Subclass (Child Class) → derived class
* Inheritance allows child classes to reuse properties and behaviors of the parent class.
* In Java, inheritance is achieved using the extends keyword.

### Example : The E-Commerce Product Catalog 
* The Goal: Share common logic across different types of objects to avoid repeating code.

* The Scenario: Build a catalog for a store. Create a base class Product.

* Why it works: All products have a name and price. But an Electronics product has a warrantyPeriod, while Clothing has size and material.

* The Practice: * Put name, price, and getDiscountedPrice() in the Product class.

* * Have Electronics and Clothing inherit from it.

* Key Lesson: You write the "price logic" once in the parent, and every child gets it for free.

```java
import java.util.*;
import java.lang.*;
import java.io.*;

class Product {
    String name;
    double price;

    public double getdiscount(double proprice){
        return price - (price * proprice / 100);
    }
}

class Electronic extends Product {
    int month ;
}

class Clothing extends Product {
    String size;
    String material;
}

public class Main
{
    public static void main (String[] args) throws java.lang.Exception
    {
        //your code here
        Electronic phone = new Electronic();
        phone.name= "iphone";
        phone.price = 60000;
        phone.month = 12;

        Clothing pant = new Clothing();
        pant.name ="silk";
        pant.size = "XXL";
        pant.price = 1200;


        System.out.println(phone.name + " " + "discount" + " " + phone.getdiscount(10));
        System.out.println(pant.name + " " +"discount" + " " +pant.getdiscount(10));

    }
}
```
---


# 3) Polymorphism :
* Polymorphism means many forms
* one method or object can behave in different ways depending on the situation.
* Simple word : Same method name, but different behavior.

## Types of Polymorphism in Java :
###  1) compile time (Method Overloading) :
    * Happens at compile time
    * Same method name
    * Different parameters
    * Example : 
``` java
        * class Calculator {
        * 
        *     int add(int a, int b) {
        *         return a + b;
        *     }
        * 
        *     int add(int a, int b, int c) {
        *         return a + b + c;
        *     }
```
### 2)runtime (Method Overriding) :
    * Happens at runtime
    * Parent & Child class required
    * Same method name + same parameters
    * Uses Inheritance
    * Example :
``` java
        * class Product {
        *     void showPrice() {
        *         System.out.println("Product price");
        *     }
        * }
        * 
        * class Mobile extends Product {
        *     @Override
        *     void showPrice() {
        *         System.out.println("Mobile price is 20,000");
        *     }
        * }
```
## Main Example :
* The Goal: Use a single "action" that behaves differently depending on the object.

* The Scenario: Create an interface or abstract class called PaymentMethod with a method processPayment(amount).

* Why it works: A CreditCard processes payment by hitting a bank API; UPI (common in India) might use a QR code scan; PayPal uses an email login.

* The Practice: * Create classes for CreditCard, UPIPayment, and Wallet.

* In your main code, create a list of PaymentMethod objects. Loop through them and call .processPayment() on each.

* Key Lesson: The "calling" code doesn't need to know how the payment happens, just that it can happen.

``` java
    * import java.util.*;
    * import java.lang.*;
    * import java.io.*;
    * 
    * 
    * interface  PaymentMethod {
    *     void processPayment(double amount);
    * }
    * 
    * class creaditecard implements PaymentMethod {
    *     @Override
    *     public void processPayment(double amount){
    *         System.out.println("payment is starting with creaditecard" + " " + amount);
    *     }
    * }
    * 
    * class upi implements PaymentMethod {
    *     @Override
    *     public void processPayment(double amount){
    *         System.out.println("pyment is strting with upi" + " " + amount);
    *     }
    * }
    * 
    * class wallet implements PaymentMethod {
    *     @Override
    *     public void processPayment(double amount){
    *         System.out.println("pyment is starting with wallet "+" "+ amount);
    *     }
    * }
    * 
    * public class Main
    * {
    *     public static void main (String[] args) throws java.lang.Exception
    *     {
    *         //your code here
    *         List<PaymentMethod> list = new ArrayList<>();
    * 
    *         list.add(new upi());
    *         list.add(new creaditecard());
    *         list.add(new wallet());
    * 
    *         for(PaymentMethod pay : list){
    *             pay.processPayment(500);
    *         }
    *     }
    * }
```
---

# 4) Abstraction :
* Abstraction means hiding implementation details and showing only essential features
* It focuses on what an object does, not how it does it
* Simple words: User ko sirf functionality dikhti hai, internal logic hidden hota hai

##  Types of Abstraction in Java :
###  1)Abstract Class :
    * Provides partial abstraction
    * Can have:
        * Abstract methods (without body)
        * Concrete methods (with body)
    * Object cannot be created directly
    * Child class extends abstract class
    * Abstract methods must be overridden
    * Example :
``` java
        * abstract class Animal {
        * 
        *     abstract void sound();   // abstract method
        * 
        *     void eat() {             // concrete method
        *         System.out.println("Eating is good");
        *     }
        * }
        * 
        * class Dog extends Animal {
        * 
        *     @Override
        *     void sound() {
        *         System.out.println("Dog barks");
        *     }
        * }
```

### 2) Interface :
    * Provides full abstraction
    * All methods are incomplete by default
    * Methods are public abstract
    * Variables are public static final
    * Object cannot be created
    * Class implements interface
    * Supports multiple inheritance
    * Example :
``` java 
        * interface Animal {
        *     void sound();
        * }
        * 
        * class Dog implements Animal {
        * 
        *     @Override
        *     public void sound() {
        *         System.out.println("Dog barks");
        *     }
        * }
```
### Main Example :
* The Goal: Hide complex internal logic and show only simple "buttons" to the user.

* The Scenario: Create a SmartDevice abstract class with a method powerOn().

* Why it works: When you turn on a SmartTV, it has to connect to Wi-Fi and load an OS. When you turn on a SmartBulb, it just sends current to a filament.

* The Practice: * Define the "what" in an abstract class (e.g., abstract void start()).

* Implement the "how" inside the specific device classes.

* The user of your class should only see the start() button, never the initializeWiFi() or voltageCheck() methods.

* Key Lesson: Abstraction reduces the "mental load" for whoever uses your code.

``` java
    * import java.util.*;
    * import java.lang.*;
    * import java.io.*;
    * 
    * abstract class SmartDevice {
    *     abstract void powerOn();
    * }
    * 
    * class SmartTV extends SmartDevice {
    * 
    *      @Override
    *     void powerOn() {
    *         initializeWiFi();
    *         loadOS();
    *         System.out.println("Smart TV is ON");
    *     }
    * 
    *     private void initializeWiFi(){
    *         System.out.println("connect wifi");
    *     }
    * 
    *     private void loadOS(){
    *         System.out.println("loadin this time");
    *     }
    * }
    * 
    * class SmartBulb extends SmartDevice {
    *     @Override
    *     void powerOn() {
    *         voltageCheck();
    *         System.out.println("Smart Bulb is ON");
    *     }
    * 
    *     private void voltageCheck() {
    *         System.out.println("Voltage check completed");
    *     }
    * }
    * 
    * public class Main
    * {
    *     public static void main (String[] args) throws java.lang.Exception
    *     {
    *         //your code here
    *         SmartDevice tv = new SmartTV();
    *         SmartDevice bulb = new SmartBulb();
    * 
    *         tv.powerOn();
    *         bulb.powerOn();
    *     }
    * }
    