Let's talk about open closed principle with a touch of strategy pattern.
Open closed principle is the "O" letter of the acronym SOLID, that represents general guidelines on how you design your projects.
Strategy pattern is a part of the design patterns, that regards to more specific example of solutions to commons types of requirements.
On this example we will use the strategy pattern to help us learn the Open Closed principle.
Let's go.

Open closed means that the class you are creating should be opened to be extended but closed to be modificated.
It means you can't keep comming to change the function, every time your business rules changes.

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
  
      public function calculateFuelConsumption(string $kmdistance)
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
