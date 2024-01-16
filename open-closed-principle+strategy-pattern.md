Let's talk about open closed principle with a touch of strategy pattern.
Open closed principle is the "O" letter of the acronym SOLID, that represents general guidelines on how you design your projects.
Strategy pattern is a part of the design patterns, that regards to more specific example of solutions to commons types of requirements.
On this example we will use the strategy pattern to help us learn the Open Closed principle.
Let's go.

Open closed means that the class you are creating should be opened to be extended but closed to be modified.
It means you can't keep changing the function or the class, every time your business rules changes.

Strategy pattern is a behavioral design that lets you select an algorithm at runtime. 
It allows you to dynamically change the behavior of an object by encapsulating it into different strategies.

Let me explain with examples:
# Code before OPEN CLOSE and STRATEGY PATTERN
```
<?php 
namespace Logistics\AutoConsumption;
use Logistics\auto\Moto;
use Logistics\auto\Car;

  class AutoConsumption
  {
      public function __construct(
          protected string $autotype,
          protected Moto $moto,
          protected Car $car
      ) {
          # code...
      }
  
      public function calculateFuelConsumption(int $kmdistance)
      {
  
          if ($this->autotype === 'moto') {
              $this->moto->CalculateMotoConsumption($kmdistance)
          }
  
          if ($this->autotype === 'car') {
              $this->car->CalculateCarConsumption($kmdistance)
          }
      }
  
  }
```

```
<?php 
namespace Logistics\auto\Moto;


  class Moto
  {
      public function __construct(
          protected string $kmconsumption,
      ) {
          $this->kmconsumption = 20;
      }
  
      public function CalculateMotoConsumption(int $kmdistance)
      {
          return $this->kmconsumption *  $kmdistance;
      }
  
  }
```

```
<?php 
namespace Logistics\auto\Car;


  class Car
  {
      public function __construct(
          protected string $kmconsumption,
      ) {
          $this->kmconsumption = 8;
      }
  
      public function CalculateCarConsumption(int $kmdistance)
      {
          return $this->kmconsumption *  $kmdistance;
      }
  
  }
```

Here we don't need to be super smart to notice that every time I have one more Auto category in my business rules, I will have to change this function.
Other problem is, if the moto class changes the name of the function, it will surely break the code.
Also, this code is very coupled, it means that every time I instantiate it will be creating a strong coupling level.

Now let's refactor the code using the Open Closed principle and Strategy pattern:

Firts of all we need to create an Interface, so all the Autos categories will have to follow the same contract.

```
<?php

namespace Logistics\Interface\IAuto;

interface IAuto
{
    public function CalculateConsumption(int $kmdistance): int;
}
```

Every class that implements this interface should implement all the functions that come with it, if we are going to follow Liskhov substitution also (from another angle).

Now we should create the auto classes that will implement it.

```
<?php 
namespace Logistics\auto\Moto;
use Logistics\Interface\IAuto;

  class Moto implements IAuto
  {
      public function __construct(
          protected string $kmconsumption,
      ) {
          $this->kmconsumption = 20;
      }
  
      public function CalculateConsumption(int $kmdistance)
      {
          return $this->kmconsumption *  $kmdistance;
      }
  
  }
```

```
<?php 
namespace Logistics\auto\Car;
use Logistics\Interface\IAuto;

  class Car implements IAuto
  {
      public function __construct(
          protected string $kmconsumption,
      ) {
          $this->kmconsumption = 8;
      }
  
      public function CalculateConsumption(int $kmdistance)
      {
          return $this->kmconsumption *  $kmdistance;
      }
  
  }
```
Now all auto categories classes are following the same contract, and they are not allowed to change the name of the functions and add new functions to the classes, according to the principles we are following.
So the problem of breaking the code is eliminated.

What about the strategy?

```
<?php 
namespace Logistics\AutoConsumption;
use Logistics\Interface\IAuto;

  class AutoConsumption implements IAuto
  {
      public function __construct(
          protected IAuto $auto,
      ) {

      }
  
      public function CalculateConsumption(int $kmdistance)
      {
          return $this->auto->CalculateConsumption($kmdistance)
      }
  
  }
```
As we can see, the AutoConsumption class doesn't depend on any external class anymore. It doesn't know nothing about "auto" classes, it just receive an entity of type IAuto, as a dependency injection.
Now this class is totally decoupled, doesn't matter how many new "auto" categories we need to create.
You won't need to change this class to add new categories, it is OPENED TO BE EXTENDED BUT CLOSED TO DE MODIFIED.

And how it is going to select the algorithm at runtime?
```
<?php 
use Logistics\AutoConsumption;
namespace Logistics\auto\Moto;
namespace Logistics\auto\Car;

  class Index implements AutoConsumption
  {
      protected AutoConsumption $motoConsumption;
      protected AutoConsumption $carConsumption;
  
      public function CalculateMotoConsumption(int $kmdistance)
      {
          return $this->motoConsumption = new AutoConsumption(
            new Moto()
          )
      }

        public function CalculateCarConsumption(int $kmdistance)
      {
          return $this->motoConsumption = new AutoConsumption(
            new Car()
          )
      }
  }
```

