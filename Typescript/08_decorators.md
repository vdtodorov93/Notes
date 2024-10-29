# Decorators
## Definition
```typescript
function Logger(logString: string) {
    return function(constructor: Function) {
        console.log(logString);
        console.log(constructor);
    }
}

function WithTemplate(template: string, hookId: string) {
    return function(constructor: any) {
        console.log('Rendering template')
        const hookEl = document.getElementById(hookId);
        const p = new constructor();
        if (hookEl) {
            hookEl.innerHTML = template;
            hookEl.querySelector('h1')!.textContent = p.name;
        }
    }
}

@Logger('Logging-person')
@WithTemplate('<h1> My Person Object </h1>', 'app')
class Person {
    name = 'Max'

    constructor() {
        console.log('Creating person object...');
    }
}
```

## Order of execution
In the example on the top, the execution would be bottom up - so first the `WithTemplate`, then the `Logger`. But only the inner `function`. The outer definition would be vice versa.

## Property decorators

```typescript

function Log(target: any, propertyName: string | Symbol) {
    console.log('Property decorator');
    console.log(target, propertyName);
}

@Log
private _price: number;
```
## Accessor decorator
```typescript
function Log2(target: any, name: string, descriptor: PropertyDescriptor) {
    console.log('Accessor decorator!');
    console.log(target);
    console.log(name);
    console.log(descriptor);
}

    @Log2
    set price(val: number) {
        if(val > 0) {
            this._price = val;
        }
    }
```

## Method decorator
```typescript
function Log3(target: any, name: string | Symbol, descriptor: PropertyDescriptor) {
    console.log('Method decorator!');
    console.log(target);
    console.log(name);
    console.log(descriptor);
}

@Log3
getPriceWithTax(@Log4 tax: number) {
    return this.price * (1 + tax);
}
```

## Parameter decorator
```typescript
function Log4(target: any, name: string | Symbol, position: number) {
    console.log('Param decorator!');
    console.log(target);
    console.log(name);
    console.log('Position: ' + position);


@Log3
getPriceWithTax(@Log4 tax: number) {
    return this.price * (1 + tax);
}
```

## Execution order
They are executed only when class is defined. Not event listeners when code is executed (e.g. instantiate a class or call a method).

## Autobind
```typescript
function Autobind(_: any, __: string, descriptor: PropertyDescriptor) {
    const originalMethod = descriptor.value;
    const adjDescriptor: PropertyDescriptor = {
        configurable: true,
        enumerable: false,
        get() {
            const boundFn = originalMethod.bind(this);
            return boundFn;
        },
    };
    return adjDescriptor;
}

class Printer {
    message = 'This works!';
    
    @Autobind
    showMessage() {
        console.log(this.message);
    }
}
```