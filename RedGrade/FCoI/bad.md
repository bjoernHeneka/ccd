## Bad
```php
class Animal{}
class FourLeggedAnimal extends Animal{
    private $leg1 = 1;
    private $leg2 = 1;
    private $leg3 = 1;
    private $leg4 = 1;
    
    public function getLeg1(){ return $this->leg1; }
    public function getLeg2(){ return $this->leg2; }
    public function getLeg3(){ return $this->leg3; }
    public function getLeg4(){ return $this->leg4; }
    
}
class FourLeggedAnimalWithTail extends FourLeggedAnimal{
    private $tail = 1;
    public function getTail(){ return $this->tail; }
}
class Cat extends FourLeggedAnimalWithTail{}

```