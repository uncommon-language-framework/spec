# Array Specification

Arrays in the ULR are implemented as pointers of elements of the specified type. For reference types, arrays are simply pointers to `void*` in the target C/C++, and since the size of value types are known at compile time, arrays of value types are simply pointers to `sizeof_ValueType` where `sizeof_ValueType` is a class/struct type whose size is equivalent to the size of the value type it represents. Thus, arrays implemented in the ULR are identical to C/C++ arrays, **with one important caveat -- ULR arrays contain four extra bytes of space preceding the array containing an `int` which holds the size of the array**. This holds the size and differs from null-termination of arrays because it avoids iteration to retrieve the size and allows for zeroed default value type instances without accidentally terminating the array. To alleviate confusion, a diagram of both a reference type and value type array for a 32-bit system is shown below. Each `[]` is a byte.

## Array of Reference Type Instances
```
-- pointer starts here --
[]    |
[]    | -- These bytes hold the size of the array
[]    | --/
[]    |
-- 0th index starts here --
[]    |
[]    | -- These four bytes point to an object
[]    | --/
[]    |
-- 1st index here --
[]    |
[]    | -- These four bytes point to an object
[]    | --/
[]    |
```


## Array of Value Type Instances

Each value type instance here has a size of 6 bytes

```
-- pointer starts here --
[]    |
[]    | -- These bytes hold the size of the array
[]    | --/
[]    |
-- 0th index starts here --
[]    |
[]    | -- These six bytes are a value object
[]    | --/
[]    |
[]    |
[]    |
-- 1st index here --
[]    |
[]    | -- These six bytes are a value object
[]    | --/
[]    |
[]    |
[]    |
```