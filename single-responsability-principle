This is the first letter principle because it is obvious, when you learn it, you can't figure out how you
built things with a lot of responsabilities inside the same class or function (it was because you were a Junior).
To summarizes this, each class, function or method must have only one responsability.
Simple like this, ONE only. You have to avoid building GOD CLASSES (a class that knows too much).

```
Class ChangeLists: 
  @abstractmethod
  def add(element);
    pass
    
  @abstractmethod
  def remove(index);
  pass
  
  @abstractmethod
  def unlink(list);
  pass

  @abstractmethod
  def CalculateTotal(list) -> int;
    pass

  @abstractmethod
  def PrintOrderedItems(list);
    pass
    
```

This is a fool example, just to show that if you have a class named CHANGELists, why are you Calculating anything or Printing things inside of it?
What can yout avoid with this principle?
Lack of cohesion, with a class assuming a responsabiliy that is not its own;
A big level of dependencies, making the code hard to give maintenance and fragile;
Hard to test, because you will have to mock a lot of things;
And will be hard to reuse the code.

So, with SRP we can refactor our code this way:

```
Class ChangeLists: 
  @abstractmethod
  def add(element);
    pass
    
  @abstractmethod
  int remove(index);
  pass
  
  @abstractmethod
  def unlink(list);
  pass

Class OperationsWithLists: 
  @abstractmethod
  def CalculateTotal(list) -> int;
    pass

Class PrintLists: 
  @abstractmethod
  int PrintOrderedItems(list);
    pass
    
```

I think two words that summarize this are Organization and Cohesion.
