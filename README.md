# data.union-find

A Clojure implementation of the Union-Find data structure.

## Usage

Make a new union-find data structure containing its arguments as singleton sets:

    user=> (def uf (union-find 1 2 3 4 5))
    user=> uf
    {5 [5], 4 [4], 3 [3], 2 [2], 1 [1]}

Union two sets:

    user=> (def uf (connect uf 2 3))
    user=> uf
    {5 [5], 4 [4], 2 [3 2], 1 [1]}

Getting the canonical element of a set can change the internals of the data structure,
due to an optimization called path compression. Therefore, get-canonical returns two
objects: the updated data structure, and the requested canonical element. Get
the canonical element of an element:

    user=> (get-canonical uf 3)
    [{5 [5], 4 [4], 2 [3 2], 1 [1]} 2]

You can use a union-find data structure as a function like you would a map. The
result is nil if the element hasn't been added, or the element's canonical element
if it has. It does not perform the path compression optimization, and just returns
the canonical element.

    user=> (uf 3)
    2
    user=> (get uf 3)
    2

    user=> (uf 10)
    nil

    user=> (uf 10 :not-found)
    :not-found

You can add new elements to the data structure with conj:

    user=> (conj uf 8)
    {8 [8], 5 [5], 4 [4], 2 [3 2], 1 [1]}


## License

Copyright © 2012 Jordan Lewis

Distributed under the Eclipse Public License, the same as Clojure.
