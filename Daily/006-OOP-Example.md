# 1 Vehicle Rental System in Java

```java
class Vehicle {
    String brand;
    String model;
    private int rent_per_day;

    public Vehicle(String brand, String model, int rent_per_day) {
        this.brand = brand;
        this.model = model;
        this.rent_per_day = rent_per_day;
    }

    public int getRentPerDay() {
        return rent_per_day;
    }

    public void setRentPerDay(int rent_per_day) {
        this.rent_per_day = rent_per_day;
    }

    public int calculate_rent(int days) {
        return rent_per_day * days;
    }
}

class Car extends Vehicle {
    int num_doors;

    public Car(String brand, String model, int rent_per_day, int num_doors) {
        super(brand, model, rent_per_day);
        this.num_doors = num_doors;
    }

    @Override
    public int calculate_rent(int days) {
        int total = getRentPerDay() * days;
        if (days > 5) {
            total = total - (total * 10 / 100); // 10% discount
        }
        return total;
    }
}

class Bike extends Vehicle {
    int engine_capacity;

    public Bike(String brand, String model, int rent_per_day, int engine_capacity) {
        super(brand, model, rent_per_day);
        this.engine_capacity = engine_capacity;
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car("Toyota", "Camry", 1000, 4);
        int carRent = car.calculate_rent(7);
        System.out.println("Car Rent: " + carRent);

        Bike bike = new Bike("Royal Enfield", "Thunderbird", 500, 350);
        int bikeRent = bike.calculate_rent(3);
        System.out.println("Bike Rent: " + bikeRent);
    }
}

✅ Expected Output :
Car Rent: 6300
Bike Rent: 1500

```


# 2 Bank Account System in Java

This example demonstrates **OOP concepts**: inheritance, encapsulation, method overriding, and polymorphism.  
It models a simple banking system with `BankAccount`, `SavingsAccount`, and `CurrentAccount`.

---

## Java Code

```java
class BankAccount {
    String accountNumber;
    String accountHoldName;
    private double balance;

    public BankAccount(String accountNumber, String accountHoldName , double balance){
        this.accountNumber = accountNumber;
        this.accountHoldName = accountHoldName;
        this.balance = balance;
    }

    public double deposite(double amount){
        balance += amount;
        System.out.println(accountHoldName + " deposited " + amount);
        return balance;
    }

    public double withdraw(double amount){
        if(amount > balance){
            System.out.println("Insufficient balance");
        } else {
            balance -= amount;
            System.out.println(accountHoldName + " withdrew " + amount);
        }
        return balance;
    }

    public double getBalance(){
        return balance;
    }
    
    public void displayBalance(){
        System.out.println(accountHoldName + "'s Balance: " + balance);
    }
}

class SavingsAccount extends BankAccount {
    double interestRate;

    public SavingsAccount(String accountNumber, String accountHoldName , double balance, double interestRate){
        super(accountNumber, accountHoldName, balance);
        this.interestRate = interestRate;
    }

    public double addInterest(){
        double interest = getBalance() * interestRate;
        deposite(interest);
        System.out.println("Interest of " + interest + " added to " + accountHoldName + "'s account");
        return getBalance();
    }
}

class CurrentAccount extends BankAccount {
    double overdraftLimit;

    public CurrentAccount(String accountNumber, String accountHoldName , double balance, double overdraftLimit){
        super(accountNumber, accountHoldName, balance);
        this.overdraftLimit = overdraftLimit;
    }

   @Override
    public double withdraw(double amount){
        if(amount > getBalance() + overdraftLimit){
            System.out.println("Insufficient funds, overdraft limit exceeded for " + accountHoldName);
        } else {
            // Reduce balance (balance can go negative up to overdraftLimit)
            double newBalance = getBalance() - amount;
            // Use setter logic via deposit negative
            super.deposite(-amount);
            System.out.println(accountHoldName + " withdrew " + amount + " (Current balance: " + getBalance() + ")");
        }
        return getBalance();
    }
}

public class Main {
    public static void main(String[] args){
        // Savings Account Test
        SavingsAccount sa = new SavingsAccount("SA123", "Alice", 1000, 0.05);
        sa.deposite(200);       
        sa.addInterest();     
        sa.displayBalance();   

        System.out.println("-------------------------");

        CurrentAccount ca = new CurrentAccount("CA456", "Bob", 500, 200);
        ca.withdraw(600);      
        ca.withdraw(200);      
        ca.deposite(300);      
        ca.displayBalance();   
    }
}

✅ Expected Output :
Alice deposited 200
Alice deposited 60.0
Interest of 60.0 added to Alice's account
Alice's Balance: 1260.0
-------------------------
Bob withdrew 600.0 (Current balance: -100.0)
Bob withdrew 200.0 (Current balance: -300.0)
Bob deposited 300
Bob's Balance: 0.0