# Intersection types

```typescript
type Admin = {
    name: string;
    privileges: string[];
};

type Employee = {
    name: string;
    startDate: Date;
}

type ElevatedEmployee = Admin & Employee;

const e1: ElevatedEmployee = {
    name: 'Max',
    privileges: ['create-server'],
    startDate: new Date()
}

type Combinable = string | number;
type Numeric = number | boolean;
type Universal = Combinable & Numeric; // it will be just the intersection - number

```

# Type Guards
You can check property names in types
```typescript
type UnknownEmployee = Employee | Admin;
function printEmployeeInformation(emp: UnknownEmployee) {
    console.log('Name: ' + emp.name);
    if('privileges' in emp) {
        console.log('Privileges: ' + emp.privileges);
    }
    if('startDate' in emp) {
        console.log('Start Date: ' + emp.startDate);
    }
}

```
You can use `instanceof` for classes, but not interfaces
```typescript

class Car {
    drive() {
        console.log('Driving...');
    }
}

class Truck {
    drive() {
        console.log('Driving truck..');
    }
    loadCargo(amount: number) {
        console.log('Loading Cargo... ' + amount);
    }
}

type Vehicle = Car | Truck
const v1 = new Car();
const v2 = new Truck();

function useVehicle(vehicle: Vehicle) {
    vehicle.drive();
    if(vehicle instanceof Truck) {
        vehicle.loadCargo(100);
    }
}
```

# Discriminated Unions
For interfaces we can
```typescript
interface Bird {
    type: 'bird';
    flyingSpeed: number;
}

interface Horse {
    type: 'horse';
    runningSpeed: number;
}

type Animal = Bird | Horse;

function moveAnimal(animal: Animal) {
    let speed;
    switch(animal.type) {
        case 'bird':
            speed =  animal.flyingSpeed;
            break;
        case 'horse':
            speed = animal.runningSpeed;
            break;
    }
    console.log('Moving at speed: ' + speed);
    
}
```

# Type casting
```typescript
const input = <HTMLInputElement>document.getElementById('user-input')!;
const input = document.getElementById('user-input')! as HTMLInputElement;
```

# Index properties
```typescript
interface ErrorContainer { // { email: 'Not a valid email', username: 'Must start with char'}
    id: string;
    [prop: string]: string;
}
```

# Function Overload
Have to add them before the method definition.

```typescript
function add2(a: number, b: number): number;
function add2(a: string, b: string): string;
function add2(a: Combinable, b: Combinable) {
    if (typeof a == 'string' || typeof b == 'string') {
        return a.toString() + b.toString()
    }
    return a + b;
}
```

# Optional chaining
```typescript
const fetchedUserData = {
    id: 'u1',
    name: 'Max',
    job: {title: 'CEO', description: 'My company'}
}

console.log(fetchedUserData?.job?.title);
```

# Nullish Coalescing
`??` would coalesce if `null` or `undefined`
```typescript
const userInput = '';
const storedData = userInput ?? 'Default';
```
`||` would coalesce if false-ish, e.g. `null`, `undefined`, `''`
```typescript
const userInput = '';
const storedData = userInput || 'Default';
```
