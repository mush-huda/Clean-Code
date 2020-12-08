# Clean-Code # 
This is a summary of the famous book "Clean Code-A Handbook of Agile Software Craftsmanship" by Robert C. Martin
### Chapter 2 - Meaningful Names ###
### Use Intention-Revealing Names ###
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
#### Use Searable Names ####
* Single-letter names and numeric constants are difficult to locate across a body of text. Use searchable names like `WORK_DAYS_PER_WEEK = 5` instead of `i = 5`
#### Avoid Encodings ####
#### Interfaces and Implementations ####
#### Avoid Mental Mapping ####
#### Class Names ####
#### Method Names ####
#### Don't be Cute ####
#### Pick One Word per Concept ###
#### Don't Pun ####
#### Don't Solution Domain Names ####
#### Don't Problem Domain Names ####
#### Add Meaningful Context ####
#### Don't Add Gratuitous Context ####
## Chapter 3 - Functions ## 

## Chapter 4 - Comments ## 

## Chapter 5 - Formatting ## 

## Chapter 6 - Objects and Data Structures ## 

## Chapter 7 - Error Handling ## 

## Chapter 8 - Boundaries ## 

## Chapter 9 - Unit Tests ## 

## Chapter 10 - Classes ## 

## Chapter 11 - Systems ## 

## Chapter 12 - Emergence ## 

## Chapter 13 - Concurrency ## 

## Chapter 14 - Successive Refinement ## 

## Chapter 15 - JUnit Internals ## 

## Chapter 16 - Refactoring SerialDate ## 

## Chapter 17 - Smells and Heuristics ## 
