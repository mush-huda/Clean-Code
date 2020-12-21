# Clean-Code # 
This is a summary of the famous book "Clean Code-A Handbook of Agile Software Craftsmanship" by Robert C. Martin
### Chapter 2 - Meaningful Names ###
#### Use Intention-Revealing Names ####
* The name of the variable, function, or class should tell you why it exists, what it does, and how it is used. 
* If a name requires a comment, then the name does not reveal its intent.
#### Avoid Disinformation ####
* Avoid leaving false clues that obscure the meaning of code. For example, Do not refer to a grouping of accounts as an `accountList` unless it's actually a `List`. It may lead false conclusions. So `accountGroup` or `bunchOfAccount` would be better choice. 
* Beware of using names which vary in small ways. Example: `ControllerFOrEfficientHandlingOfStrings` `ControllerForEfficientStorageOfStrings`
#### Make Meaningful Distinctions ####
* Number-series namings(a1,a2,.. aN) are noninformative. 
* The word `variable` should never appear in a variable name. The word `table` should never appear in a table name. 
#### Use Pronounceable Names ####
* Don't use `genymdhms`(generation date,year,month,day,hour,min,sec) but use pronounceable names like `generationTimestamp`
#### Use Searchable Names ####
* Single-letter names and numeric constants are difficult to locate across a body of text. Use searchable names like `WORK_DAYS_PER_WEEK = 5` instead of `i = 5`
#### Avoid Encodings ####
* If you must do encoding then encode implementation. Example: Don't encode interfaces like `IShapeFactory`. Keep interface as it is `ShapeFactory` and encode implementation `ShapeFactoryImp`.
#### Avoid Mental Mapping ####
* Don't use variable names that has speacial meaning to you. Spell out the whole word.
* Clarity is king!
#### Class Names ####
* Classes and objects should have noun or noun phrase name like `Customer`, `WikiPage`, `Account`.
* Avoid words like `Manager`, `Processor`, `Data`, or `Info`n the name of a class. 
* A class name should not be a verb.
#### Method Names ####
* Methods should have verb or verb phrase names like `postPayment`, `deletePage`, or `save`
* When constructors are overloaded, use static factory methods with names that describe the argument:
`Complex fulcrumPoint = Complex.FromRealNumber(23.0);` is better than `Complex fulcrumPoint = new Complex(23.0);`
#### Don't be Cute ####
 Don't use funny names or culture-specific names. Don't use `whack()` to mean `kill()`.
#### Pick One Word per Concept ###
* Pick one word for one abstract concept and stick with it. It's confusing to have `fetch`, `retrieve`, and `get`as equivalent methods of different classes. 
#### Don't Pun ####
* Avoid using the same word for two purposes. Let's say we have `add` methods in different classes that recreate a new value by adding two existing values. Now if we are writing a new class that has a method that puts its single parameter into collection. Now, to call the new method `add` would be pun. Call that method `insert` or `append` instead.
#### Don't Solution Domain Names ####
* If the people who will read your code are programmers then go ahead and use CS terms, algorithm names, pattern names, math terms, etc. 
* The name `AccountVisitor` means a great deal to a programmer who is familiar with the *Visitor Patter.*
#### Don't Problem Domain Names ####
* The code that has more to do with problem doamin concepts should have names drawn from the problem domain. 
#### Add Meaningful Context ####
* You need to place names in context for your reader by enclosing them in well-named classes, functions, or namespaces. When all else fails, then prefixing the name may be necessary as a last resort.
#### Don't Add Gratuitous Context ####
* Add no more context to a name than is necessary. In an imaginary application called "Gas Station Deluxe", it is bad idea to prefix every class with `GSD`like `GSDAccountAddress`. 
## Chapter 3 - Functions ## 
#### Small! ####
* The first rule of functions is that the should be small. 
* The second rule of functions is that they should be smaller than that.
##### Blocks and Indenting #####
* Blocks within `if` statements, `else` statements, `while` statements, and so on should be one line long. Probably that line should be a function call. Not only does this keep the enclosing function small. but it also adds documentary value because the function called within the block can have a nicely descriptive name. 
#### Do One Thing ####
* Functions should do one thing. They should do it well. The should do it only.
##### Sections within Functions #####
* Functions that do one thing cannot be reasonably divided into many sections. 
#### One Level of Abstraction per Function ####
* In order to make sure our functions are doing "one thing", we need to make sure that the statements within our function are all at the same level of abstraction. 
* Mixing levels of abstraction within a function is always confusing. 
##### Reading Code from Top to Bottom: The Stepdown Rule #####
* *The Stepdown Rule:* We want the code to read like a top-down narrative. We want every function to be followed by those at the next level of abstraction so that we can read the program, descending on level of abstraction ata a time as we read down the list of functions. 
#### Switch Statements ####
* It's hard to make a `switch` statment that does on thing. By their nature, `switch` statements always do `N` things.

```
public Money calculatePay(Employee e) throws InvalidEmployeeType {
  switch(e.type)
     case COMMISSIONED:
        return calculateCommissionedPay(e);
     case HOURLY:
        return calculateHourlyPay(e);
     case SALARIED:
        return calculateSalariedPay(e);
     default:
        throw new InvalidEmployeeType(e.type);
}
```
* There are several problems with this function: it's large, it does more than one thing, it has more than one reason to change, it must change whenever new types are added.
* The solution to this problem is to bury the `switch` statement in the basement of an `ABSTRACT FACTORY`, and never let anyone see it. The factory will use the `switch` statment to create appropriate instances of the derivatives of `Employee`, and the various functions, such as `calculatePay`, `isPayday`, and `deliverPay`, will be dispatched polymorphically through the `Employee` interface.
#### Use Descriptive Names ####
* The smaller and more focused a function is, the easier it is to choose a descriptive name. 
* A long descriptive name is better than a short enigmatic name. 
* Don't be afraid to spend time choosing a name. Indeed, you should try several diffent names and read the code with each in place. 
* Be consitent in your names. Use the same phrases, nouns, and verbs in the function names you choose for your modules. For example: `includeSetupAndTeardownPages`, `includeSetupPages`, `includeSuiteSetupPages`.
#### Function Arguments ####
* The ideal number of arguments for a function is zero(niladic). Next comes one(monadic), followed closely by two(dyadic). Three arguments(triadic) should be avoided where possible. 
* More that three(polyadic) arguments require very special justification - and then shouldn't be used anyway.
* Arguments are even harder for a testing point of view. 
* Using an output argument instead of a return value is confusing and hard to understand. Avoid them. 
##### Common Monadic Forms #####
* There are two very common reasons to pass a single argument into a function. 
* You may be asking a question about that argument, as in `boolean fileExists("MyFile")`
* Or you may be operating on that argument, transforming it into something else and returning it. For example, `InputStream fileOpen("MyFile")` transforms a file name `String` into an `InputStream` return value.
* A somewhat less common, but still very useful form for a monadic function is an event. In this form there is an input argument but no output argument. The overall program is meant to interpret the function call as an event and use the argument to alter the state of the system. For example, `void passwortAttemptFailedNtime(int attempts)`. 
##### Flag Arguments #####
* Flag arguments are ugly. Passing a boolean into a function is a truly terrible practive. 
* It immediately complicates the signature of the method, loudly proclaiming that this function does more than one thing. It does one thing if the flag is `true` and another if the flag is `false`.
##### Dyadic Functions #####
* A function with two arguments is harder to understand than a monadic function. 
* There are times when two arguments are appropriate. For example, `Point(0, 0)` is perfectly reasonable. Cartesian points naturally take two arguments. The two arguments in this case are ordered components of a single value. 
* When possible convert dyads into monads. For example, `writeField(outputStream, name)` can be transformed as `writeField(name)` by making the `outputStream` a member variable of the class so that you don't have to pass it. Or you might extract a new class like `FieldWriter` that takes the `outputStream` in its constructor and has a `write` method.  
##### Triads #####
* Functions that take three arguments are significantly harder to understand than dyads. Think very carefully before creating a triad. 
##### Argument Objects #####
* When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be wrapped into a class of their own.
```
  Circle makeCircle(double x, double y, double radius);
  Circle makeCircle(Point center, double radius);
```
##### Verbs and Keywords #####
* In the case of monad, the function and argument should form a very nice verb/noun pair. For example, `write(name)` is very evocative. Whatever the "name" thing is, it is being "written".
#### Have No Side Effects ####
* A function should not have hidden side effects. A function `checkPassword(String userName, String password)` should only check if the password is correct or not. It should not do any hidden tasks like `Session.initialize()`.
* In this case we might rename the function `checkPasswordAndInitializeSession`, though that certainly violates Single Responsibility Principle. 
##### Output Arguments #####
#### Command Query Separation ####
#### Prefer Exceptions to Returning Error Codes ####
##### Extract Try/Catch Blocks #####
##### Error Handling Is One Thing #####
##### The Error.java Dependency Magnet #####
#### Structured Programming ####
#### How Do You Write Functions Like This? ####
#### Conclusion ####
#### SetupTeardownIncluder ####

## Chapter 4 - Comments ## 

## Chapter 5 - Formatting ## 

## Chapter 6 - Objects and Data Structures ## 

## Chapter 7 - Error Handling ## 

## Chapter 8 - Boundaries ## 

## Chapter 9 - Unit Tests ## 

## Chapter 10 - Classes ## 
#### Class Organzation ####
* According to Java Convention, a class should begin with a list of variables. 
    * `public static constants` should come first.
    * Then `private static` variables.
    * Followed by `private` instance variables.
    * There is seldom a good reason to have `public` variables.
##### Encapsulation #####
* It's good to keep variables and utility functions `private` but sometimes we need to make them `protected` so that they can be accessed by a test. But loosening encapsulation is always a last resort. 
#### Classes Should Be Small! ####
* The first rule of classes is that they should be small.
* The second rule of classes is tht they should be smaller than that.
* With functions we measured size by counting physical lines. With classes we use a different measure. We count *responsibilities*
* The name of the class should describe what responsibilities it fulfills.
* We should also be able to write a brief description of the class in about 25 words, without using the words "if", "and", "or", or "but". 
#### The Single Responsibility Principle ####
* The *Single Responsibiliy Principle(SRP)* states that a class or module should have one and only one *reason to change*.
* We want out systems to be composed of many small clsses, not a few large ones. Each small class encapsulates a single responsibility, has a single reason to change, and collaborates with a few others to achieve the desired system behaviors.
#### Cohesion ####
* Classes should have a small number of instance variables. Each of the methods of a class should manipulate one or more of those variables. 
* In general the more variables a nethod manipulates the more cohesive that method is to its class.
* A class in which each variable is used by each method is maximally cohesive. 
* We would like cohesion to be high. When cohesion is high, it means that the methods and variables of the class are co-dependent and hang together as a logical whole.
#### Maintaining Cohesion in Many Small Classes ####
* You should try to separate the variables and methods into two or more classes such that the newclasses are more cohesive. 
* When classes lose cohesion, split them!
#### Organizing for Change ####
* For most systems, change is continual.
* We want to structure our systems so tat we muck with as little as possible when we update them with new or changed features. 
* In an ideal system, we incorporate new features by extending the system, not by making modifications to existing code. 
* *Open-Closed Principle(OCP)* states that classes should be open for extension but closed for modification. 
#### Isolating from Change ####
* Needs will change, therefore code will change. 
* A Client class depending upon concerete details is at risk when those details change. We can introduce interfaces and abstract classes to help isolate the impact of those details. 
* Dependencies upon concrete details challenges for testing our system. 
* Instead of designing `Portfolio` so that it directly depends upon `TokyoStockExchange`, we create an Interface, `StockExchange`, that declares a single method. 

```
public interface StockExchange {
    Money currentPrice(String symbol)
}

public Portfolio {
    private StockExchange exchange;
    public Portfolio(StockExchange exchange) {
       this.exchange = exchange; 
    }
}
```
* By minimizing coupling in this way, our classes adhere to another class design principle known as *Dependency Inversion Principle(DIP)*. DIP says that our classes should depend upon abstraction, not on concrete details. 

## Chapter 11 - Systems ## 

## Chapter 12 - Emergence ## 

## Chapter 13 - Concurrency ## 

## Chapter 14 - Successive Refinement ## 

## Chapter 15 - JUnit Internals ## 

## Chapter 16 - Refactoring SerialDate ## 

## Chapter 17 - Smells and Heuristics ## 
