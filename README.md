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
* You should try to separate the variables and methods into two or more classes such that the newclasses are more cohesive. 
#### Maintaining Cohesion in Many Small Classes ####
#### Organizing for Change ####
#### Isolating from Change ####


## Chapter 11 - Systems ## 

## Chapter 12 - Emergence ## 

## Chapter 13 - Concurrency ## 

## Chapter 14 - Successive Refinement ## 

## Chapter 15 - JUnit Internals ## 

## Chapter 16 - Refactoring SerialDate ## 

## Chapter 17 - Smells and Heuristics ## 
