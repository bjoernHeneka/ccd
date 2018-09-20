## Good
```php   
class Cat extends AbstractLifeform{
    private $legs;
    private $tail;
    
    public function __construct() {
        $this->legs = new Leg(4);
        $this->tail = new Tail();
    }
    
    public function getLegs(){ return $this->legs; }
    public function getTail(){ return $this->tail; }
}
```