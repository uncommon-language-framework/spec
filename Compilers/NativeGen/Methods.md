# Compiler Method Naming Conventions

Compilers should name C/C++ functions generated from ULF code with the following naming conventions:

If not an operator overload, `overload<overnumber>_ns<nsnumber>_Namespace_Split_By_Underscores_cl<classnumber>_Class_Names_Split_By_Underscores_<methodname>` where overnumber is the number of the overload (in the order of declaration) starting from zero, nsnumber is the number of namespaces (e.g. `System` would be one namespace, while `System.Collections` would yield two namespaces), and classnumber is the same as nsnumber except in the fact that it counts nested classes rather than namespaces.

If an operator overload,
`overload<number>_operator<operatorname>_ns<nsnumber>_Namespace_Split_By_Underscores_cl<classnumber>_Class_Names_Split_By_Underscores_<methodname>` where number is the number of the overload (in the order of declaration) starting from zero, operatorname is the name of the operation, nsnumber is the number of namespaces (e.g. `System` would be one namespace, while `System.Collections` would yield two namespaces), and classnumber is the same as nsnumber except in the fact that it counts nested classes rather than namespaces.

Note that the prefix `special_<ident>` can also be added to the beginning of ANY name to denote a special symbol to be recognized by the compiler (e.g. a runtime extension method inject to a native type, such as the runtime-added array methods).

If a method is not overloaded at all, its overload number is `0`.