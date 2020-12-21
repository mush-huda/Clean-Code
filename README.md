# Clean-Code # 
This is a summary of the famous book *"Clean Code-A Handbook of Agile Software Craftsmanship"* by *Robert C. Martin*. 
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
* In the days before object oriented programming it was sometimes necessary to have output arguments. However, much of the need for output arguments disappears in OO languages because `this` is intended to act as an output argument. 
* Anything that forces you to check the function signature is equivalent to a double-take. It's cognitive break and should be avoided. 
#### Command Query Separation ####
* Functions should either do something or answer something, but not both. 
* Either your function should change the state of an object, or it should return some information about that object. Doing both often leads to confusion. 
* Always separate the command from the query so that the ambiguity cannot occur. 
#### Prefer Exceptions to Returning Error Codes ####
* Returning error codes from command functions is a subtle violation of command query separation. It promotes commands being used as expressions in the predicates of `if`statements.
##### Extract Try/Catch Blocks #####
* Try/Catch blocks are ugly in thier own right. They confuse the structure of the code and mix error processing. So it's better to extract the bodies of the `try` and  `catch` blocks out into functions of their own. 
##### Error Handling Is One Thing #####
* Error handling is one thing. Thus, a function that handles errors should do nothing else.
* This implies that if the keyword `try` exists in a function, it should be the very first word in the function and that there should be nothing after the `catch/finally` blocks.
##### The Error.java Dependency Magnet #####
* Returning error codes usually implies that there is some class or enum in which all the error codes are defined. 
* Classes like this are a *dependency management*. Many other classes must import and use them. Thus, when the `Error enum` changes, all those other classes need to be recompiled and redeployed. 
* When you use exceptions rather than error codes, then new exceptions are *derivatives* of the exception class. They can be added without forcing any recompilation or redeployment. 
#### Don't Repeat Yourself ####
* Duplication may be the root of all evil in software. 
* Encapsulate the duplicates and create smaller fucntions.
* This is *DRY* principle. 
#### Structured Programming ####
* Edsger Dijkstra's rules of structured programming states that every function, and every block within a function, should have one entry and one exit. 
* Following these rules means that there should only be one `return` statement in a function, no `break` or `continue` statements in a loop, and never,ever, any `goto` statements.
* It is only in larger functions that such rules provide significant benefits. 
* If you keep your functions small, then the occasional multiple `return`, `break`, or `continue` statement does no harm.
#### How Do You Write Functions Like This? ####
* Don't expect to write functions in a perfect way from the start. Refactor, refactor and refactor!
* Master programmers think of systems as stories to be told rather that programs to be written. 

## Chapter 4 - Comments ##
* If out programming languages were expressive enough, or if we had the talent to subtly wield those languages to express out intent, we would not need comments very much -- perhabs not at all.
* The proper use of comments is to compensate for our failure to express ourself in code. 
* So when you find yourself in a position where you need to write a comment, think it through and see whether there isn't  some way to turn the tables and express yourself in code. 
* Inaccurate comments are far worse than no comments at all. They delude and mislead. 
* Truth can only be found in one place: *the code*. It is the only source of truly accurate information.
#### Comments Do Not Make Up For Bad Code ####
* One of the more common motivations for writing comments is bad code. We write a module and we know it is confusing and disorganized. So we tend to write comment. 
* Rather than spend your time writing the comments that explain the mess you have made, spend it cleaning that mess. 
#### Explain Yourself in Code ####
* Don't:
```
  if ((employee.flags & HOURLY_FLAG) && (employee.age > 65))
```
Do:
```
  if (employee.isEligibleForFullBenefits())
```
#### Good Comments ####
* Some comments are necessary or beneficial:
##### Legal Comments #####
* Copyright and authorship statements are necessary and reasonable things to put into a comment at the start of each source file.
##### Informative Comments #####
* It's sometimes useful to provide basic information with a comment. Still try to use the name of the function to convey the information where possible.
##### Explanation of Intent #####
* Sometimes a comment can provide the intent behind a decision.
##### Clarification #####
* In general it is better to find a way to make obscure arguments or return value clear in its own right; but when its part of the standard library, or in code that you cannot alter, then it is just helpful to translate the meaning of some obscure argument or return value into something that's readable.
##### Warning of Consequences #####
* Sometimes it is useful to warn other programmers about certain consequences. 
##### TODO Comments #####
* `TODO`s are jobs that the programmer thinks should be done but for some reason can't do at the moment. It might be a reminder to delete a deprecated feature or a plea for someone else to look at a problem. 
##### Amplification #####
* A comment may be used to amplify the importance of something that may otherwise seem inconsequential.
##### Javadocs in Public APIs #####
* If you are writing a public API, then you should certainly write good javadocs for it. 
#### Bad Comments ####
##### Mumbling #####
* If you decide to write a comment, then spend the time necessary to make sure it is the best comment you can write.
##### Redundant Comments #####
* Don't write redundant comments. 
##### Misleading Comments #####
* Don't write comments that are not accurate. Don't give false information to the reader.
##### Mandated Comments #####
* It's just plain silly to have a rule that says that every function must have a javadoc, or every variable must have a comment. 
* Comments like this just clutter up the code, propagate lies, and lend to general confusion and disorganization.
##### Journal Comments #####
* Sometimes people add a comment to the start of a module every time they edit it. These comments accumulate as a kind of journal, or log, of every change that has ever been made. 
* Source code control systems can take care of these things. Don't add journal comments into your code. 
##### Noise Comments #####
* Noise comments restate the obvious and provide no new information.
```
/** The day of the month **/
   priavate int dayOfMonth;
```
##### Don't Use a Comment When You Can Use a Function or Variable #####
* Don't:
```
 if (smodule.getDependSubsystems().contains(subSysMod.getSubSytem()))
```
 Do:
 
 ```
  ArrayList moduleDependees = smodule.getDependSubsystems();
  String ourSubSystem = subSysMod.getSubSystem();
  if (moduleDependees.contains(ourSubSystem))
 ```
##### Position Markers #####
* Sometimes programmers like to mark a particular position in a source file. They are called banners.
* Use banners carefully. 
##### Closing Brace Comments #####
* Sometimes programmers put special comments on closing braces. 
* The might make sense for long functions with deeply nested strutures. But small and encapsulated functions don't need comments. They are self explaining.
##### Attributes and Bylines #####
* Don't add bylines like `/* Added by Rick */`. 
* Source code control system can handle these things.
##### Commented-Out Code #####
* Few practices are as odious as commenting-out code. Don't do this!!
* Again, source code control systems will remember the code for us. We don't have to comment it out any more. Just delete the code!
##### HTML Comments #####
* If comments are going to be extracted by some tool (like Javadoc) to appear in Web page, then it should be the responsibility of that tool, and not the programmer, to adorn the comments with appropriate HTML.
##### Nonlocal Information #####
* If you must write a comment, then make sure it describes the code it appears near. Don't offer systemwide information in the context of a local comment. 
##### Too Much Information #####
* Don't put interesting historical discussions or irrelevant descriptions of details into your comments.
##### Inobvious Connection #####
* The purpose of a comment is to explain code that does not explain itself. It is a pity when a comment needs its own explanation.
##### Function Headers #####
* Short functions don't need much description. A well-chosen name for a small function that does one thing ususally better than a comment header.
##### Javadocs in Nonpublic Code #####
* Generating javadoc pages for the classes and functions inside a system is not generally useful, and the extra formality of the javadoc comments amounts to little more than cruft and distraction. 
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
