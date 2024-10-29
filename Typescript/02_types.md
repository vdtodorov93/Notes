# Tuples
Tuples are strongly typed, but `person.role.push('admin');` is allowed, which breaks the tuple. 
`person.role[1] = 10;` is not allowed.

```typescript
const person: {
    name: string;
    age: number;
    hobbies: string[];
    role: [number, string];
} = {
    name: 'Maximilian',
    age: 30,
    hobbies: ['Sports'],
    role: [2, 'author']
};

person.role.push('admin');
person.role[1] = 10;
```

# For loop
```typescript
for(const hobby of person.hobbies) {
    console.log(hobby.toUpperCase())
}
```

# Enums
Could be any case. The first value is 0 by default, we can assign a value and all follow up values will be incremented by 1, or we can assign numeric values to all variants.
```typescript
enum Role {
    ADMIN = 5, READ_ONLY, AUTHOR
};
```

# Union Types
```typescript
function combine(input1: number | string, input2: number | string) {
    let result;
    if(typeof input1 === 'number' && typeof input2 === 'number') {
        result = input1 + input2
    } else {
        result = input1.toString() + input2.toString()
    }
    return result;
}

```

# Type Litteral
```typescript
resultConversion: 'as-number' | 'as-text'
```

# Type Alias
```typescript
type Combinable = number | string
```

# Functions

This is how to define a function type
```typescript
let combineValue: (a: number, b: number) => number;
let combine: Function; // any function can be assigned here
```

# Callbacks
```typescript
function addAndHandle(n1: number, n2: number, cb: (num: number) => void) {
    cb(n1 + n2);
}

addAndHandle(10, 15, (result) => {
    console.log(result);
})
```

# Unknown
```typescript
let userInput: unknown = 'input'
let userInput2: any = 'input2'
let userName: string;

userName = userInput; // compile error, cannot assign unknown to string
if(typeof userInput2 === 'string') {
    userName = userInput2;
} // compiles !
```

# Never
If exception is always thrown by a function, it can return `never` type.
```typescript
function generateError(message: string, code: number): never {
    throw {message: message, errorCode: code};
}
```