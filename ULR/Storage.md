# Storage & Storage Size (64-bit System/Runtime)

This document covers the various *storage sizes* for different objects in various storage *containers*, regions in memory where an object or a reference to an object can be stored.

Storage *containers* are defined as follows:
- `local` - a stack-based local variable in a function
- `apl` - a local variable in a function passed via the function arguments
- `field` - a field of an object *or* type (static *or* instance)
- `stack` - a single slot on the evaluation stack as used in UIL
- `boxed` - the region of memory allocated for value types when *boxed* into reference types

## Reference Types

The storage size for any reference type object in any container (`local`, `field`, `apl`, `stack`) is *always* the pointer size of the system (8 bytes in this case), as all reference objects are always stored as pointers to the start of the object.

## Value Types

The storage size for value types in various containers within the ULR differs based on the runtime size of the value type.

When loaded by the runtime, a value type's size is a equivalent to the sum of the `field` storage sizes of its instance members, padded to the next greatest or equal number of bytes from the list `1+8n`, `2+8n`, `4+8n`, or `8n` bytes, where `n` is an nonnegative integer. This means that for any value type represented by an internal runtime object `ULR::Type* valtype`, `valtype->size % 8` must be equal to either `0`, `1`, `2`, `4`.

### Small Value Types

This section covers the storage specification for value types whose size is less than or equal to the word size (8 bytes).
- `local` - `valtype->size` bytes
- `field` - `valtype->size` bytes
- `apl` - 8 bytes (padded)
- `stack` - 8 bytes (padded)
- `boxed` - 8+`valtype->size` bytes (need 8 byte header for type ptr)

### Large Value Types

This section covers the storage specification for value types whose size is greater than the word size (8 bytes).
- `field` - `valtype->size` bytes
- `local` - `valtype->size` bytes
- `stack` - 8 bytes (pointer to where object is located in memory)
- `apl` - 8 bytes (pointer to where object is located in memory)
- `boxed` - 8+`valtype->size` bytes (need 8 byte header for type ptr)