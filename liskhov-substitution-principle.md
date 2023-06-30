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
interface List {
    void add(int element);
    int get(int index);
    void unlink();
}

class ArrayList implements List {
    // Implementations for add() and get() methods
}

class LinkedList implements List {
    // Implementations for add(), get() and unlink() methods
}

// Usage
void unlinkList(List list) {
  list.unlink()
}

ArrayList arrayList = new ArrayList();
LinkedList linkedList = new LinkedList();

unlinkList(linkedList); // It works too!
unlinkList(arrayList);  // It won't work!

```

See what happens when you call unlinkList passing an ArrayList by parameter, knowing that you didn't implement this method? 
It will certainly brake your program.


Now, look at code that uses is using Liskhov:

```
interface List {
    void add(int element);
    int get(int index);
}

class ListWithLinks implements List {
    void unlink(){
      //unlink the list (of course this is an example)
    };
}

class ArrayList implements List {
    // Implementations for add() and get() methods
}

class LinkedList implements ListWithLinks {
    // Implementations for add(), get() and unlink() methods
}

// Usage
void unlinkList(ListWithLinks list) {
  list.unlink()
}

void printList(List list) {
    for (int i = 0; i < list.size(); i++) {
        System.out.println(list.get(i));
    }
}

ArrayList arrayList = new ArrayList();
LinkedList linkedList = new LinkedList();

printList(arrayList);  // It works!
printList(linkedList); // It works too!
unlinkList(linkedList); // It works too!
```

These examples demonstrate how the Liskov Substitution Principle allows for the interchangeability of objects within a class hierarchy, 
enabling code reuse and flexibility in object-oriented programming.
