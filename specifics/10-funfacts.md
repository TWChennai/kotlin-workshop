### Funfact: Backing Field

A property with a backing field will store the value in the form of a field. That field makes storing value in memory possible. 

- An example of such property is the first and second properties of Pair. That property will change the in-memory representation of Pair.

A property without a backing field will have to store their value in other ways than directly storing it in memory. It must be computed from other properties, or, the object itself. 

- An example of such property is the indices extension property of List, which is not backed by a field, but a computed result based on size property. So it won't change the in-memory representation of List.