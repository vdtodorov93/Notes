# Classes
## Define a class
```typescript
class Department {
    name: string;

    constructor(n: string) { //constructor
        this.name = n;
    }

    describe() {
        console.log('Department');
    } // this is how you create a method
}

new Department("HR"); // instantiate
```

## Optimize constructor and members
You don't need to repeat all members in the constructor. You can just define them in the constructor with the public/private modifiers.
```typescript
   
    private employees: string[] = [];

    constructor(private id: string, public name: string) {
        
    }
```

## Getters and Setters
```typescript
    private reports: string[];

    get mostRecentReport() {
        if(this.reports) {
            return this.reports;
        } else return [];
    }

    set mostRecentReport(reports) {
        if(reports) {
            this.reports = reports;
        } else throw new Error('Empty reports')
    }
```

## Static methods
```typescript
static fiscalYear = 2020;
static createEmployee(name: string) {
    return new Department('idomg', name)
}
```

## Abstract classes
Abstract methods do not have implementation
```typescript
abstract class Department {
    abstract describe(this: Department): void;
}
```

## Singletons
You can have a `private` constructor.

```typescript
class AccountingDepartment {
    private static instance: AccountingDepartment;

    private constructor(private id: string) {

    }

    static getInstance() {
        if(AccountingDepartment.instance) {
            return this.instance;
        }
        this.instance = new AccountingDepartment('id);
        return this.instance;
    }
}
```

# Intefaces

```typescript
interface Greetable {
    name: string;
    

    greet(phrase: string): void;
}

class Person implements Greetable {
    name: string;
    age = 30;

    constructor(n: string) {
        this.name = n;
    }

    greet(phrase: string): void {
        console.log(phrase + ' ' + this.name);
    }
}
```

## Function types
```typescript
type AddFn = (a: number, b: number) => number;
interface AddFn {
    (a: number, b: number): number
}
let add: AddFn;


add = (n1: number, n2: number) => {
    return n1 + n2;
}
```

## Optional props
```typescript
interface Named {
    readonly name: string;
    outputName?: string;
}
```