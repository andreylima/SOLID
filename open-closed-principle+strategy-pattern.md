Let's talk about open closed principle with a touch of strategy pattern.
Open closed principle is the "O" letter of the acronym SOLID, that represents general guidelines on how you design your projects.
Strategy pattern is a part of the design patterns, that regards to more specific example of solutions to commons types of requirements.
On this example we will use the strategy pattern to help us learn the Open Closed principle.
Let's go.

Open closed means that the class you are creating should be opened to be extended but closed to be modificated.
It means you can't keep comming to change the function, every time your business rules changes.

Strategy pattern is a behavioral design, that lets you select an algorithm at runtime. 
It allows you to dynamically change the behavior of an object by encapsulating it into different strategies.

Let me explain with examples:
# Code before OPEN CLOSE and STRATEGY PATTERN
```
<?php 
namespace Logistics\Consumption;
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

Here we don't need to be super smart to notice that every time I have one more Auto in my business rules, I will have to change this function.
Other problem is, if the moto class changes the name of the function, it will surely break the code.
Also, this code is very coupled, it means that every time I instantiate I will be creating a strong coupling level.

Now let's refactor the code using the Open Closed principle and Strategy pattern:

Firts of all we need to create and Interface, so all the Autos will have to follow the same contract (every class the implements this interface should implement all the functions that come with it, kind of Liskhov substition from another angle).





