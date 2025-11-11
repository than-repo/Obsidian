Both are used to define types, but interface is mainly for objects and supports declaration merging—meaning you can define the same name multiple times to merge properties, which is very useful when extending libraries. Interface also uses 'extends' for inheritance.

On the other hand, type alias is more flexible; it can define primitives, unions, intersections, or mapped types. Type uses '&' to combine, but does not support merging.

For example, interface is suitable for defining classes or APIs, while type is used for complex types like a union of string and number.