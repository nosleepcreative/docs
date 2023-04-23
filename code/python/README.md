# Python

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
