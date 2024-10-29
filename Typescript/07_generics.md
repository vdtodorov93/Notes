# Generics
```typescript
function merge<T extends Object, U extends Object> (obj1: T, obj2: U) {
    return Object.assign(obj1, obj2);
}

console.log(merge({name:"vasko"}, {age:30}))
```
## Keyof
```typescript
function extract<T extends Object, U extends keyof T> (obj T, key U) {
    return obj[key];
}
```

## Partial
Partial wraps a type with optional fields. It can be cast when all fields are filled.
```typescript
interface A {
    a: number,
    b: string
}

let obj: A = {}
obj.a = 20;
obj.b = 'omg';
return obj as A
```

## Readonly

```typescript
const a: Readonly<string[]> = ['asd', 'omg'];
a.push('12') //error
```