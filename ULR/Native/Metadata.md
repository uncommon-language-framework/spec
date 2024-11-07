# ULR Metadata Specification

Metadata is crucial to the loading of native assemblies in the ULR. Each assembly DLL must export two metadata symbols: `char* ulrmeta` and [`void* ulraddr[]`](ULRAddr.md). The `ulrmeta` symbol should be a char pointer to a string literal containing all type information of the assembly to be read by the ULR Loader, in the following format:

### Typenames

All class names in ULR metadata should be written in the following format: `[Namespace.Name]ClassName`. For example, the class `System.String` should be written as `[System]String`. Array types will have their square brackets at the end of the typename. For example, the array type `System.String[]` should be written as `[System]String[]`. Generic type declarations, like `System.Collections.Generic.List<T>` should be written without the `T`, like `[System.Collections.Generic]List<>`, and if there is more than one type parameter, a comma should be added in between the angle brackets for every extra type parameter. For example, `MyClass<T, V>` would end up looking like `[]MyClass<,>`. Complete generic types should contain typenames within the angle brackets. For example, `MyClass<int, string>` would end up as `[]MyClass<[System]Int32, [System]String>`. Void should be represented as `[System]Void`.

### Parameter Lists

All parameter lists should be enclosed within parentheses and comma separated. The list should only contain typenames. For example, the parameter list of `void Method(int argOne, MyClass argTwo)` would look like this in ULR metadata: `([System]Int32, []MyClass)`.

### Metadata Format

The metadata should begin right with one of the classes declared in the assembly. The class declaration should be written with access modifier letters followed by the type modifier letter (e.g. class/interface/struct) followed by the typename in metadata format. For all modifier letters, see [Modifier Letters](./ModifierLetters.md).

Following the typename, there should be a semicolon (`:`) and then the typename of the base class. Following the typename of the base class, there should be a comma and then a comma-separated list of implemented interfaces. If the class does not implement any interfaces, the comma is STILL REQUIRED at the end of the base class typename. The interface list should NOT end with a comma.

Following the interface list, a dollar sign (`$`) is required followed by the size of the type. For reference types, this should include the actual size of the type plus the pointer size (for the object header). After the size, a semicolon (`;`) must appear.

From here, the class' attributes can be listed according to the member types below (all member declarations should end with a semicolon (`;`), no exceptions):

### Constructors

Begin a constructor declaration with `.ctor` immediately followed by a space. The space should be followed by modifier letters and then an argument list directly after the modifiers.

### Destructors

The destructor declaration is simply `.dtor`. Note that the semicolon termination rule still applies.

### Methods


### Fields


### Properties

Every class declaration should end with a newline to signify the end of the class.