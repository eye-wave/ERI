# 襟 Eri 

Eri - **Extendable record interface**

Elegant file format that enhances the traditional CSV structure by introducing static typed values, comments, nested properties, arrays and even custom types.

## Features

### Static types
Eri supports a range of default static types, ensuring robust and statically-typed data representation. The following types are natively supported:

- **Unsigned Integers:** `u8`, `u16`, `u32`
- **Signed Integers:** `i8`, `i16`, `i32`
- **Floating Point Numbers:** `f32`, `f64`
- **Boolean:** `bool`
- **String:** `string`
> default column type is **string**, so you can avoid using `:string`

### Comments

Eri allows you to add comments to your files using the `#` symbol. This feature enables you to document your datasets, providing context and explanations for better understanding.

### Arrays

Eri supports arrays, allowing you to organize data in a structured manner. **Arrays can only contain values of default supported types**.

Use square brackets (`[]`) in the header to represent arrays, enhancing the versatility of your datasets.

### Nested Properties

With Eri, you can represent nested properties using a dot (`.`) in the header. This feature enables you to organize data structures complex than just Records. Use nested properties to create rich, structured representations of your information.

## Example

```eri
# Sample Eri File
name:string,age:i32,grades:[]f64,isActive:bool,contact.address.city:string,contact.address.zip:u32 # Column types

John Doe,25,[85.5, 90.0, 78.3],true,New York,10001
Jane Smith,30,[92.3, 88.5, 94.1],false,San Francisco,94105
Bob Johnson,22,[78.9, 80.2, 85.0],true,Seattle,98101
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
