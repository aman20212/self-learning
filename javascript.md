https://gist.github.com/Ak-Shaw/360b4ec2a19c4e94cc2dcf0874d4eae2

**Sealing an object globally**<br />
Property descriptors work at the level of individual properties.

There are also methods that limit access to the whole object:<br />

**Object.preventExtensions(obj)**
Forbids the addition of new properties to the object.<br />
**Object.seal(obj)**
Forbids adding/removing of properties. Sets configurable: false for all existing properties.<br />
**Object.freeze(obj)**<br />
Forbids adding/removing/changing of properties. Sets configurable: false, writable: false for all existing properties.
And also there are tests for them:<br />

**Object.isExtensible(obj)**
Returns false if adding properties is forbidden, otherwise true.<br />
**Object.isSealed(obj)**
Returns true if adding/removing properties is forbidden, and all existing properties have configurable: false.<br />
**Object.isFrozen(obj)**
Returns true if adding/removing/changing properties is forbidden, and all current properties are configurable: false, writable: false.

------------------------------------------------------------------------------*****----------------------------------------------------------------------

**Design Pattern in JavaScript**<br />
Design Patterns can be categorised in 3 categories: <br />
a. Creational <br />
b. Structural <br />
c. Behavioral <br />

**1. Creational Design Pattern**<br />
**Factory design Pattern**
object creation at centralized location. Resusability. Helps in object creation <br />
/*
    Factory Design Pattern -> https://www.youtube.com/watch?v=kuirGzhGhyw
    Author: DevSage (Youtube) -> https://www.youtube.com/DevSage
*/

function Developer(name)
{
  this.name = name
  this.type = "Developer"
}

function Tester(name)
{
  this.name = name
  this.type = "Tester"
}

function EmployeeFactory()
{
  this.create = (name, type) => {
    switch(type)
    {
      case 1:
        return new Developer(name)
      case 2:
        return new Tester(name)
    }
  }
}

function say()
{
  console.log("Hi, I am " + this.name + " and I am a " + this.type)
}

const employeeFactory = new EmployeeFactory()
const employees = []

employees.push(employeeFactory.create("Patrick", 1))
employees.push(employeeFactory.create("John", 2))
employees.push(employeeFactory.create("Jamie", 1))
employees.push(employeeFactory.create("Taylor", 1))
employees.push(employeeFactory.create("Tim", 2))

employees.forEach( emp => {
  say.call(emp)
})

**Singleton Pattern** <br />
This is also a creational pattern. It comes in handy when we want to limit object instance to 1. <br />
/*
    Singleton Design Pattern -> https://www.youtube.com/watch?v=JKNjfDCNPa4
    Author: DevSage (Youtube) -> https://www.youtube.com/DevSage
*/

const Singleton = (function(){
  let pManager

  function ProcessManager() { /*...*/ }

  function createProcessManager()
  {
    pManager = new ProcessManager()
    return pManager
  }

  return {
      getProcessManager: () =>
      {
        if(!pManager)
          pManager = createProcessManager()
        return pManager
      }
  }
})()

const singleton = Singleton.getProcessManager()
const singleton2 = Singleton.getProcessManager()

console.log(singleton === singleton2) // true
https://github.com/pkellz/devsage/blob/master/DesignPatterns/SingletonPattern.js


**Strategy Pattern** <br />
is a pattern where we encapsulates group of closely related strategies (functions). They allow us to swap strategies in and out easily. <br />
https://github.com/pkellz/devsage/blob/master/DesignPatterns/StrategyDesignPattern.js <br />

/*
    Strategy Design Pattern -> https://www.youtube.com/watch?v=SicL4fYCz8w
    Author: DevSage (Youtube) -> https://www.youtube.com/DevSage
*/

function Fedex(pkg)
{
  this.calculate = () =>
  {
    // Fedex calculations ...
    return 2.45
  }
}

function UPS(pkg)
{
  this.calculate = () =>
  {
    // UPS calculations ...
    return 1.56
  }
}

function USPS(pkg)
{
  this.calculate = () =>
  {
    // USPS calculations ...
    return 4.5
  }
}

function Shipping()
{
  this.company = ''
  this.setStrategy = company =>
  {
    this.company = company
  }
  this.calculate = pkg => {
    return this.company.calculate(pkg)
  }
}

const fedex = new Fedex()
const ups = new UPS()
const usps = new USPS()
const shipping = new Shipping()
const pkg = { from: "Alabama", to: "Georgia", weight: 1.56 } // Dummy package

shipping.setStrategy(fedex)
console.log("Fedex: " + shipping.calculate(pkg))

shipping.setStrategy(ups)
console.log("UPS: " + shipping.calculate(pkg))

shipping.setStrategy(usps)
console.log("USPS: " + shipping.calculate(pkg))
