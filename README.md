# 襟 Eri 

Eri - **Extendable record interface**

Elegant file format that enhances the traditional CSV structure by introducing static typed values, comments, nested properties, arrays and even custom types.

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

With Eri, you can represent nested properties using a dot (`.`) in the header. This feature enables you to organize data structures more complex than just Records. Use nested properties to create rich, structured representations of your information.

## Example

```eri
# Sample Eri File
name:string,age:u8,grades:f32[],isActive:bool,contact.address.city:string,contact.address.zip:u32 # Column types

John Doe,25,[85.5, 90.0, 78.3],true,New York,10001
Jane Smith,30,[92.3, 88.5, 94.1],false,San Francisco,94105
Bob Johnson,22,[78.9, 80.2, 85.0],true,Seattle,98101
...
```

equals to:

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
```

equals to:

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
