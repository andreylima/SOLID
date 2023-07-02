* I will explain liskhov substitution principle with my words and give easy to understand examples.

If you have a function that is expecting a type of class, and you have more classes that implement this type,
this function will have to accept all of this classes without breaking the program. This includes the possibility of this function run all the methods 
of the class it is expecting, so if you have some methods in the superclass that you won't use in the subclasses,
you can't just ignore them and don't use. 

The name is substitution because you have to be able to substitute the class expected by any of the classes that inherit from it, without any error.

If you are not going to use, you have to fix it, reestructuring your abstractions and in some cases using some of the other SOLID principles as
Open-closed principle and Interface Segregation Principle.

A simple example of an error that is possible to happen if you don't use this principle:

```
from abc import ABC, abstractmethod

class List(ABC):
    @abstractmethod
    def add(self, element):
        pass

    @abstractmethod
    def get(self, index):
        pass

    @abstractmethod
    def unlink(self):
        pass

class ArrayList(List):
    def add(self, element):
        # Implementation for add() method
        pass

    def get(self, index):
        # Implementation for get() method
        pass

class LinkedList(List):
    def add(self, element):
        # Implementation for add() method
        pass

    def get(self, index):
        # Implementation for get() method
        pass

    def unlink(self):
        # Implementation for unlink() method
        pass

# Usage
class ManageLists:
    def unlinkList(list_obj : List):
        list_obj.unlink()

arrayList = ArrayList()
linkedList = LinkedList()

ManageLists.unlinkList(linkedList)  # It works!
ManageLists.unlinkList(arrayList)   # It won't work!

```

See what happens when you call unlinkList passing an ArrayList by parameter, knowing that you didn't implement this method? 
It will certainly brake your program.


Now, look at a code that is using Liskhov principles:

```
from abc import ABC, abstractmethod

class List(ABC):
    @abstractmethod
    def add(self, element):
        pass

    @abstractmethod
    def get(self, index):
        pass


class ListWithLinks(List)
    @abstractmethod
    def unlink 
      pass

class ArrayList List(List)
    // Implementations for add() and get() methods

class LinkedList(ListWithLinks)
    // Implementations for add(), get() and unlink() methods

// Usage
class ManageLists:
    def unlinkList(list_obj : ListWithLinks) 
      list_obj.unlink()
    
    def printList(list_obj : List) 
        for i in range(len(list)):
            print(list.get(i))

arrayList = ArrayList()
linkedList = LinkedList()

ManageLists.printList(arrayList)   # It works!
ManageLists.printList(linkedList)  # It works too!
ManageLists.unlinkList(linkedList) # It works too!
```

These examples demonstrate how the Liskov Substitution Principle allows for the interchangeability of objects within a class hierarchy, 
enabling code reuse and flexibility in object-oriented programming.
