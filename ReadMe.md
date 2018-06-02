# Creational Patterns
* ## Factory Pattern:

> Create object without exposing the creation logic to the client and refer to newly created object using a common interface.



```Java
public interface Shape {
    void draw();
}
```

>> Create concrete classes implementing the same interface.

```Java
public class Rectangle implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Rectangle::draw() method.");
   }
}
```
```Java
public class Square implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Square::draw() method.");
   }
}
```

>>Create a Factory to generate object of concrete class based on given information.

```Java
public class ShapeFactory {
	
   //use getShape method to get object of type shape 
   public Shape getShape(String shapeType){
      if(shapeType == null){
         return null;
      }		
      if(shapeType.equalsIgnoreCase("CIRCLE")){
         return new Circle();
         
      } else if(shapeType.equalsIgnoreCase("RECTANGLE")){
         return new Rectangle();
         
      } else if(shapeType.equalsIgnoreCase("SQUARE")){
         return new Square();
      }
      
      return null;
   }
}
```

>>Use the Factory to get object of concrete class by passing an information such as type.

```Java
public class FactoryPatternDemo {

   public static void main(String[] args) {
      ShapeFactory shapeFactory = new ShapeFactory();

      //get an object of Circle and call its draw method.
      Shape shape1 = shapeFactory.getShape("CIRCLE");

      //call draw method of Circle
      shape1.draw();

      //get an object of Rectangle and call its draw method.
      Shape shape2 = shapeFactory.getShape("RECTANGLE");

      //call draw method of Rectangle
      shape2.draw();

      //get an object of Square and call its draw method.
      Shape shape3 = shapeFactory.getShape("SQUARE");

      //call draw method of square
      shape3.draw();
   }
}
```
* ## Singleton Pattern:

>This pattern involves a single class which is responsible to create an object while making sure that only single object gets created. This class provides a way to access its only object which can be accessed directly without need to instantiate the object of the class.

>> Create a Singleton Class.

```Java
public class SingleObject {

   //create an object of SingleObject
   private static SingleObject instance = new SingleObject();

   //make the constructor private so that this class cannot be
   //instantiated
   private SingleObject(){}

   //Get the only object available
   public static SingleObject getInstance(){
      return instance;
   }

   public void showMessage(){
      System.out.println("Hello World!");
   }
}
```

>>Get the only object from the singleton class.
```Java
public class SingletonPatternDemo {
   public static void main(String[] args) {

      //illegal construct
      //Compile Time Error: The constructor SingleObject() is not visible
      //SingleObject object = new SingleObject();

      //Get the only object available
      SingleObject object = SingleObject.getInstance();

      //show the message
      object.showMessage();
   }
}
```

* ## Builder pattern

>> Suppose we have the following class named BackAccount, but if we want to add more parameters to the constructor, things will become more complicated.
```Java
public class BankAccount {
    private long accountNumber;
    private String owner;
    private double balance;
    public BankAccount(long accountNumber, String owner, double balance) {
        this.accountNumber = accountNumber;
        this.owner = owner;
        this.balance = balance;
    }
    //Getters and setters omitted for brevity.
}
```
```Java
BankAccount account = new BankAccount(456L, "Marge", "Springfield", 100.00, 2.5);
BankAccount anotherAccount = new BankAccount(789L, "Homer", null, 2.5, 100.00);  
```

>> Instead, we can declare BankAccount like the following class. Please make sure the constructor of BankAccount is set to private.
```Java
public class BankAccount {
    public static class Builder {
        private long accountNumber; //This is important, so we'll pass it to the constructor.
        private String owner;
        private String branch;
        private double balance;
        private double interestRate;
        public Builder(long accountNumber) {
            this.accountNumber = accountNumber;
        }
        public Builder withOwner(String owner){
            this.owner = owner;
            return this;  //By returning the builder each time, we can create a fluent interface.
        }
        public Builder atBranch(String branch){
            this.branch = branch;
            return this;
        }
        public Builder openingBalance(double balance){
            this.balance = balance;
            return this;
        }
        public Builder atRate(double interestRate){
            this.interestRate = interestRate;
            return this;
        }
        public BankAccount build(){
            //Here we create the actual bank account object, which is always in a fully initialised state when it's returned.
            BankAccount account = new BankAccount();  //Since the builder is in the BankAccount class, we can invoke its private constructor.
            account.accountNumber = this.accountNumber;
            account.owner = this.owner;
            account.branch = this.branch;
            account.balance = this.balance;
            account.interestRate = this.interestRate;
            return account;
        }
    }
    //Fields omitted for brevity.
    private BankAccount() {
        //Constructor is now private.
    }
    //Getters and setters omitted for brevity.
}
```

>> Then we can create BankAccount like the flowing ones. We don't have to pass too many argument to the constructor anymore, and the code look more simple.


```JAVA
BankAccount account = new BankAccount.Builder(1234L)
            .withOwner("Marge")
            .atBranch("Springfield")
            .openingBalance(100)
            .atRate(2.5)
            .build();
BankAccount anotherAccount = new BankAccount.Builder(4567L)
            .withOwner("Homer")
            .atBranch("Springfield")
            .openingBalance(100)
            .atRate(2.5)
            .build();
```


# Structural Patterns

# Behavioral Patterns