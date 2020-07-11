#  Solid Principles

SOLID is a list of 5 software engineering principles. It is a meta acronym where each letter corresponds to another acronym:

-   S  -   SRP (Single Responsibility Principle)
-   O -   OCP (Open Closed Principle)
-   L  -   LSP (Liskov Substitution Principle)
-   I   -   ISP (Interface Segregation Principle)
-   D -   DIP (Dependency Inversion Principle)

Let's go through each of the above software engineering principles one by one:

### 1\. SRP (Single Responsibility Principle)[](https://www.callicoder.com/software-development-principles/#1-srp-single-responsibility-principle)

The SRP states that every function, class, module, or service should have a single clearly defined responsibility. In other words, A class/function/module should have [one and only one reason](https://blog.cleancoder.com/uncle-bob/2014/05/08/SingleReponsibilityPrinciple.html) to change.

But why is this important? Well, when you define your functions or classes in such a way that they're focused and responsible for a single functionality, your code becomes a lot easier to understand, maintain, and modify. Whenever you want to make any changes to a functionality, you would exactly know that single DRY(Don't Repeat Yourself) place where you have to change the code that is responsible for that functionality.

Let's understand the Single Responsibility Principle with some real-world analogies:

-   In a house, the kitchen is for cooking and bedroom is for sleeping. Both have a single clearly defined responsibility. You don't cook in the bedroom or sleep in the kitchen. When you want to eat, you go to the kitchen; and when you're feeling sleepy, you go to the bedroom. It makes things so convenient.

-   In a company, the Project managers, Engineers, HRs, Sales people, and everyone else has a clearly defined responsibility. The PMs collect requirements and track the progress of the project. The engineers write code. The Sales people are responsible for marketing and selling the product.

The SRP principle makes the code more organized. It improves the readability of the code. It also contributes a lot to reusability. If you have short and focused functions/classes, you'll be able to reuse them easily. But if you have a single function that does too many things then you wouldn't be able to use it if you only need a fraction of the functionality implemented by the function.

### 2\. OCP (Open/Closed Principle)

When we develop software, we do it in phases. We implement a bunch of functionalities, test it, and then release it to the users. Then we start implementing the next set of functionalities.

When we develop new functionalities, the last thing we want is to make changes to the existing functionality that works and is tested. We instead try to build the new functionality on top of the existing functionality.

The [Open/Closed principle](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle) is a facilitator of the above idea. It advises that we should build our functions/classes/modules in such a way that they are *open for extension*, but *closed for modification*.

-   Open for Extension

    We should be able to add new features to the classes/modules without breaking existing code. This can be achieved using inheritance and composition.

-   Closed for Modification

    We should strive not to introduce breaking changes to the existing functionality, because that would force us to refactor a lot of existing code and write a whole bunch of tests to make sure that the changes work.

### 3\. LSP (Liskov Substitution Principle)

The [Liskov Substitution Principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle) simply means that every child/derived class should be substitutable for their parent/base class without altering the correctness of the program. In other words, the objects of your subclass should behave in the same way as the objects of your superclass.

Let's understand this with an example. Let's say that you have a class called `Bird` and a subclass of it called `Penguin`.

```
class Bird {
    public void fly() {
        System.out.println("Bird flying...");
    }
    public void eat() {
        System.out.println("Bird eating...");
    }
}

class Penguin extends Bird {
    public void fly() {
       throw new UnsupportedOperationException("Can't fly.");
    }
}

class LSPTest {
    public static void main(String[] args) {
        Bird bird = new Bird();
        bird.fly();
    }
}

```

According to Liskov Substitution Principle, if you have a piece of code that uses a `Bird` object, then you should be able to replace it with a `Penguin` object and the code will still behave the same.

But, the above example violates the Liskov Substitution Principle. You can't replace an object of the `Bird` class with an object of the `Penguin` class. If you do that, the program will throw an exception.

To fix this, you could create another abstraction which captures the flying capability of a Bird -

```
class Bird {
    public void eat() {
        System.out.println("Bird eating...");
    }
}

class FlightBird extends Bird {
    public void fly() {
        System.out.println("Bird flying...");
    }
}

class FlightlessBird extends Bird {

}

```

### 4\. ISP (Interface Segregation Principle)[](https://www.callicoder.com/software-development-principles/#4-isp-interface-segregation-principle)

The [Interface Segregation Principle](https://en.wikipedia.org/wiki/Interface_segregation_principle) states that a client should never be forced to depend on methods it does not use.

And how do you achieve this? Well, By making your interfaces small and focused.

You should split large interfaces into more specific ones that are focused on a specific set of functionalities so that the clients can choose to depend only on the functionalities they need.

### 5\. DIP (Dependency Inversion Principle)[](https://www.callicoder.com/software-development-principles/#5-dip-dependency-inversion-principle)

The [Dependency Inversion Principle](https://en.wikipedia.org/wiki/Dependency_inversion_principle) tries to avoid tight coupling between software modules. It states that High-level modules should not depend on low-level modules, but only on their abstractions. In simple words, It suggests that you should use interfaces instead of concrete implementations wherever possible.

This decouples a module from the implementation details of its dependencies. The module only knows about the behavior on which it depends, not how that behavior is implemented. This allows you to change the implementation whenever you want without affecting the module itself.