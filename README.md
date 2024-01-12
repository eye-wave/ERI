# 襟 Eri 

Eri - **Extendable record interface**

Elegant file format that enhances the traditional CSV structure by introducing static typed values, comments, nested properties, arrays and custom type definitions for the parser.

## Features

### Static types
Eri supports a range of default static types, ensuring robust and statically-typed data representation. The following types are natively supported:

- Numbers
- - Unsigned integers: `u8`, `u16`, `u32`
- - Signed integers: `i8`, `i16`, `i32`
- - Floating point numbers: `f32`, `f64`
- Boolean: `bool`
- String: `string`

> default field type is **string**, so you can avoid using `:string`

### Comments

Eri allows you to add comments to your files using the `#` symbol. This feature enables you to document your datasets, providing context and explanations for better understanding.

### Arrays

Eri supports basic arrays, like number or string arrays. **Arrays can only contain values of default supported types**. Use square brackets (`[]`) in the header to represent arrays, enhancing the versatility of your datasets.

### Nested Properties

With Eri, you can represent nested properties using a dot (`.`) in the header. For example if you want to create this object in eri:
```ts
social_links: {
  youtube: string,
  instagram: string,
  linkedin: string
}
```
you'd write something like this in the header:
```
social_links.youtube:string,
social_links.instagram:string
social_links.linkedin:string
```

### Custom types / Preprocessors

Eri parser introduces *custom types*. Providing a function to the parser you can preprocess data in a way that matches your project perfectly. You could make for example a :date type which would transform timestamps into locale formatted date.

## Example

```eri
# Sample Eri File
name:string,age:u8,grades:f32[],isActive:bool,contact.address.city:string,contact.address.zip:u32 # Column types

John Doe,25,[85.5, 90.0, 78.3],true,New York,10001
Jane Smith,30,[92.3, 88.5, 94.1],false,San Francisco,94105
Bob Johnson,22,[78.9, 80.2, 85.0],true,Seattle,98101
...
```

Json output:
```json
[
  {
    "name": "John Doe",
    "age": 25,
    "grades": [85.5, 90.0, 78.3],
    "isActive": true,
    "contact": {
      "address": {
        "city": "New York",
        "zip": 10001
      }
    }
  }
  ...
]
```

See how the header can get pretty long? Eri allows you to write header fields line by line

```eri
# Sample .eri file
name
age:i32
subjects:[]string
is_active:bool

John Doe,25,["Math", "Physics", "Chemistry"],true
Jane Smith,30,["English", "History", "Art"],false
Bob Johnson,22,["Computer Science", "Statistics"],true
...
```

Json output:
```json
[
  {
    "name": "John Doe",
    "age": 25,
    "subjects": ["Math", "Physics", "Chemistry"],
    "is_active": true
  }
  ...
]
```
