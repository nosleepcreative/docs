# Python Cheat Sheet

| Syntax/Concept                                                               | Example                                                                                                    | Explanation                                                                |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Print statement                                                              | print("Hello, world!")                                                                                     | Outputs the given text to the console                                      |
| Comments                                                                     | # This is a comment                                                                                        | Comments are ignored by Python and are used to document code               |
| Multiline comment                                                            | """                                                                                                        |                                                                            |
| This is a multiline comment.                                                 |                                                                                                            |                                                                            |
| It can span multiple lines without the need for multiple comment symbols.    |                                                                                                            |                                                                            |
| You can use it to document your code or temporarily disable a block of code. |                                                                                                            |                                                                            |
| ""”                                                                          |                                                                                                            |                                                                            |
| Variables                                                                    | x = 5                                                                                                      | Variables are used to store data and can be assigned and reassigned values |
| Data types                                                                   | int, float, string, bool, list, tuple, dict, set                                                           | Different types of data that can be stored in variables                    |
| Numeric operations                                                           | +, -, \*, /, %, \*\*                                                                                       | Operators used for arithmetic operations                                   |
| Comparison operators                                                         | ==, !=, >, <, >=, <=                                                                                       | Operators used to compare values                                           |
| Logical operators                                                            | and, or, not                                                                                               | Operators used to combine and manipulate boolean values                    |
| Conditional statements                                                       | if, elif, else                                                                                             | Statements used to conditionally execute code                              |
| Loops                                                                        | for, while                                                                                                 | Statements used to iterate over a sequence of data                         |
| Functions                                                                    | def my\_func():, return                                                                                    | Blocks of code that can be called and returned                             |
| Lambda functions                                                             | lambda x: x + 1                                                                                            | Anonymous functions used for simple operations                             |
| Classes                                                                      | class MyClass:, def **init**(self):, self                                                                  | Used to define custom data types and associated functions                  |
| List methods                                                                 | append(), extend(), insert(), remove(), pop(), index(), count(), sort(), reverse()                         | Methods used to manipulate lists                                           |
| Tuple methods                                                                | count(), index()                                                                                           | Methods used to manipulate tuples                                          |
| Dictionary methods                                                           | keys(), values(), items(), get(), update(), pop(), popitem(), clear()                                      | Methods used to manipulate dictionaries                                    |
| Set methods                                                                  | add(), remove(), discard(), pop(), clear(), union(), intersection(), difference(), symmetric\_difference() | Methods used to manipulate sets                                            |

##

## Getting Started

* Corey Schafer,  [Object-Oriented Programming ](https://www.youtube.com/watch?v=ZDa-Z5JzLYM\&list=PL-osiE80TeTsqhIuOqKhwlXsIBIdSeYtc) 6 parts&#x20;
* Setting up a Python Development Environment
  * Requirements: syntax highlighting, beautification, linter,  IntelliSense: list members, parameter info, quick info, autocompletion,&#x20;
  * [Corey Schafer](https://www.youtube.com/watch?v=06I63\_p-2A4\&list=PL-osiE80TeTt66h8cVpmbayBKlMTuS55y\&index=8)

## Class

* Why? Logically group our data and functions that we can easily reuse or build upon
* **Terminology**
  * Attributes and methods - functions that is associated with class
  * A class is a blueprint for creating instances

```python
class Employee:
    pass 

# instances of a Employee classes
emp_1 = Employee()
emp_2 = Employee()
s
# unique data 
#manually variable setting - prone to human error
emp_1.first = 'Corey'
emp_1.last = 'Scafer'
emp_1.email = 'cScafer@company.com'
emp_1.pay = '50000'

emp_2.first = 'Test'
emp_2.last = 'User'
emp_2.email = 'testUser@company.com'
emp_21.pay = '60000'
######

class Employee:
    def __init__(self,first,last,pay):
        #set instance variable 
        self.first = first
        self.last = last
        self.pay =pay
        self.email = first +'.' + last + '@company.com'
        
    # each method within a class automatically takes the insance as the first argument
    # and we always call that self
    def fullname(self)
        return '{}{}'.format(self.first,self.last)
    
# better solution: runs init automatically 
emp_1 = Employee('Corey','Scafer',50000)
emp_2 = Employee('Test','User',60000)

print(emp_1.email)
print(emp_2.email)

# running actions
    #manually 
    print('{}{}'.format)emp_1.first,emp_1,last))
    
    # better 
    print(emp_1.fullname()) # notice the parenthesis as it is a method

#notes
#classes are kinda like function
# remember to put self in methods in class
    emp_1.fullname() is same as Employee.fullname(emp_1))
```
