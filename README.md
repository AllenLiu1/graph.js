graph.js
========
[![Build Status](http://img.shields.io/travis/mhelvens/graph.js.svg)](https://travis-ci.org/mhelvens/graph.js?branch=master)
[![Coverage Status](http://img.shields.io/coveralls/mhelvens/graph.js.svg)](https://coveralls.io/r/mhelvens/graph.js?branch=master)
[![npm](https://img.shields.io/npm/v/graph.js.svg)](https://www.npmjs.com/package/graph.js)
[![Bower](https://img.shields.io/bower/v/js-graph.svg)](http://bower.io/search/?q=js-graph)

*formerly known as js-graph (still called js-graph on Bower)*

`graph.js` is a javascript library for storing arbitrary data in mathematical (di)graphs,
as well as traversing and analyzing them in various ways. It was originally created to
track dependencies between options and modules. It is written in ECMAScript 6, but
auto-generated ECMAScript 5 versions are shipped with it.

If you want to run this library in an ECMAScript 5 context, it depends on the [Babel ES6 polyfill](https://babeljs.io/docs/usage/polyfill/).
For your convenience, a version is provided with this polyfill already baked in, but you also
have the option of providing it yourself.

Feedback of any kind (questions, issues, pull requests) is greatly appreciated.


Files
-----

The `dist` directory offers different files for use in different circumstances.
Use the following table to determine which file to use in your situation.

| File                                    | Description                                                                                 |
| --------------------------------------- | ------------------------------------------------------------------------------------------- |
| `graph.es6.js`                          | for use in an ECMAScript 6 context, e.g., a modern browser or transpiler                    |
| `graph.js`,<br>`graph.min.js`           | requires you to load the [Babel polyfill](https://babeljs.io/docs/usage/polyfill/) yourself |
| `graph.full.js`,<br>`graph.full.min.js` | already includes the Babel polyfill                                                         |

If you don't know which you need, you probably want `graph.full.min.js`, because it will work out-of-the-box.
But it is generally more elegant to load the polyfill yourself, especially if you use other libraries that also
depend on it.

API Documentation
-----------------


* [Graph](#Graph)
    * <ins><b>instance</b></ins>
    * [.addNewVertex(key, [value])](#Graph#addNewVertex)
    * [.setVertex(key, [value])](#Graph#setVertex)
    * [.ensureVertex(key, [value])](#Graph#ensureVertex)
    * [.addVertex(key, [value])](#Graph#addVertex)
    * [.removeExistingVertex(key)](#Graph#removeExistingVertex)
    * [.destroyExistingVertex(key)](#Graph#destroyExistingVertex)
    * [.removeVertex(key)](#Graph#removeVertex)
    * [.destroyVertex(key)](#Graph#destroyVertex)
    * [.vertexCount()](#Graph#vertexCount) ⇒ <code>number</code>
    * [.hasVertex(key)](#Graph#hasVertex) ⇒ <code>boolean</code>
    * [.vertexValue(key)](#Graph#vertexValue) ⇒ <code>\*</code>
    * [.addNewEdge(from, to, [value])](#Graph#addNewEdge)
    * [.createNewEdge(from, to, [value])](#Graph#createNewEdge)
    * [.setEdge(from, to, [value])](#Graph#setEdge)
    * [.spanEdge(from, to, [value])](#Graph#spanEdge)
    * [.addEdge(from, to, [value])](#Graph#addEdge)
    * [.ensureEdge(from, to, [value])](#Graph#ensureEdge)
    * [.createEdge(from, to, [value])](#Graph#createEdge)
    * [.removeExistingEdge(from, to)](#Graph#removeExistingEdge)
    * [.removeEdge(from, to)](#Graph#removeEdge)
    * [.edgeCount()](#Graph#edgeCount) ⇒ <code>number</code>
    * [.hasEdge(from, to)](#Graph#hasEdge) ⇒ <code>boolean</code>
    * [.edgeValue(from, to)](#Graph#edgeValue) ⇒ <code>\*</code>
    * [.vertices()](#Graph#vertices) ⇒ <code>Iterator.&lt;string, \*&gt;</code>
    * [.@@iterator()](#Graph#@@iterator) ⇒ <code>Iterator.&lt;string, \*&gt;</code>
    * [.edges()](#Graph#edges) ⇒ <code>Iterator.&lt;string, string, \*&gt;</code>
    * [.verticesFrom(from)](#Graph#verticesFrom) ⇒ <code>Iterator.&lt;string, \*, \*&gt;</code>
    * [.verticesTo(to)](#Graph#verticesTo) ⇒ <code>Iterator.&lt;string, \*, \*&gt;</code>
    * [.verticesWithPathFrom(from)](#Graph#verticesWithPathFrom) ⇒ <code>Iterator.&lt;string, \*&gt;</code>
    * [.verticesWithPathTo(to)](#Graph#verticesWithPathTo) ⇒ <code>Iterator.&lt;string, \*&gt;</code>
    * [.vertices_topologically()](#Graph#vertices_topologically) ⇒ <code>Iterator.&lt;string, \*&gt;</code>
    * [.clearEdges()](#Graph#clearEdges)
    * [.clear()](#Graph#clear)
    * [.equals(other, [eq])](#Graph#equals) ⇒ <code>boolean</code>
    * [.cycle()](#Graph#cycle) ⇒ <code>array</code>
    * [.hasCycle()](#Graph#hasCycle) ⇒ <code>boolean</code>
    * [.path(from, to)](#Graph#path) ⇒ <code>array</code>
    * [.hasPath(from, to)](#Graph#hasPath) ⇒ <code>boolean</code>
    * [.clone([tr])](#Graph#clone) ⇒ <code>[Graph](#Graph)</code>
    * [.transitiveReduction([tr])](#Graph#transitiveReduction) ⇒ <code>[Graph](#Graph)</code>
    * <ins><b>static</b></ins>
    * [.VertexExistsError](#Graph.VertexExistsError) ⇐ <code>Error</code>
        * [.vertices](#Graph.VertexExistsError#vertices) : <code>Set.&lt;{key: string, value}&gt;</code>
    * [.VertexNotExistsError](#Graph.VertexNotExistsError) ⇐ <code>Error</code>
        * [.vertices](#Graph.VertexNotExistsError#vertices) : <code>Set.&lt;{key: string}&gt;</code>
    * [.EdgeExistsError](#Graph.EdgeExistsError) ⇐ <code>Error</code>
        * [.edges](#Graph.EdgeExistsError#edges) : <code>Set.&lt;{from: string, to: string, value}&gt;</code>
    * [.EdgeNotExistsError](#Graph.EdgeNotExistsError) ⇐ <code>Error</code>
        * [.edges](#Graph.EdgeNotExistsError#edges) : <code>Set.&lt;{from: string, to: string}&gt;</code>
    * [.HasConnectedEdgesError](#Graph.HasConnectedEdgesError) ⇐ <code>Error</code>
        * [.key](#Graph.HasConnectedEdgesError#key) : <code>string</code>
    * [.CycleError](#Graph.CycleError) ⇐ <code>Error</code>
        * [.cycle](#Graph.CycleError#cycle) : <code>Array.&lt;string&gt;</code>


-----

<a name="Graph"></a>
### Graph
The main class of this library, to be used for representing a mathematical (di)graph.


-----

<a name="Graph#addNewVertex"></a>
#### *graph*.addNewVertex(key, [value])
Add a new vertex to this graph.


| Param | Type | Description |
| --- | --- | --- |
| key | <code>string</code> | the key with which to refer to this new vertex |
| [value] | <code>\*</code> | the value to store in this new vertex |

**Throws**:

- <code>[VertexExistsError](#Graph.VertexExistsError)</code> if a vertex with this key already exists


-----

<a name="Graph#setVertex"></a>
#### *graph*.setVertex(key, [value])
Set the value of an existing vertex in this graph.


| Param | Type | Description |
| --- | --- | --- |
| key | <code>string</code> | the key belonging to the vertex |
| [value] | <code>\*</code> | the value to store in this vertex |

**Throws**:

- <code>[VertexNotExistsError](#Graph.VertexNotExistsError)</code> if a vertex with this key does not exist


-----

<a name="Graph#ensureVertex"></a>
#### *graph*.ensureVertex(key, [value])
Make sure a vertex with a specific key exists in this graph. If it already exists,
do nothing. If it does not yet exist, add a new vertex with the given value.


| Param | Type | Description |
| --- | --- | --- |
| key | <code>string</code> | the key for the vertex |
| [value] | <code>\*</code> | the value to store if a new vertex is added |


-----

<a name="Graph#addVertex"></a>
#### *graph*.addVertex(key, [value])
Add a new vertex to this graph. If a vertex with this key already exists,
the value of that vertex is overwritten.


| Param | Type | Description |
| --- | --- | --- |
| key | <code>string</code> | the key with which to refer to this new vertex |
| [value] | <code>\*</code> | the value to store in this new vertex |


-----

<a name="Graph#removeExistingVertex"></a>
#### *graph*.removeExistingVertex(key)
Remove an existing vertex from this graph.


| Param | Type | Description |
| --- | --- | --- |
| key | <code>string</code> | the key of the vertex to remove |

**Throws**:

- <code>[VertexNotExistsError](#Graph.VertexNotExistsError)</code> if a vertex with this key does not exist
- <code>[HasConnectedEdgesError](#Graph.HasConnectedEdgesError)</code> if there are still edges connected to this vertex


-----

<a name="Graph#destroyExistingVertex"></a>
#### *graph*.destroyExistingVertex(key)
Remove an existing vertex from this graph, as well as all edges connected to it.


| Param | Type | Description |
| --- | --- | --- |
| key | <code>string</code> | the key of the vertex to remove |

**Throws**:

- <code>[VertexNotExistsError](#Graph.VertexNotExistsError)</code> if a vertex with this key does not exist


-----

<a name="Graph#removeVertex"></a>
#### *graph*.removeVertex(key)
Remove an existing vertex from this graph.
If a vertex with this key does not exist, nothing happens.


| Param | Type | Description |
| --- | --- | --- |
| key | <code>string</code> | the key of the vertex to remove |

**Throws**:

- <code>[HasConnectedEdgesError](#Graph.HasConnectedEdgesError)</code> if there are still edges connected to this vertex


-----

<a name="Graph#destroyVertex"></a>
#### *graph*.destroyVertex(key)
Remove a vertex from this graph, as well as all edges connected to it.
If a vertex with this key does not exist, nothing happens.


| Param | Type | Description |
| --- | --- | --- |
| key | <code>string</code> | the key of the vertex to remove |


-----

<a name="Graph#vertexCount"></a>
#### *graph*.vertexCount() ⇒ <code>number</code>
**Returns**: <code>number</code> - the number of vertices in the whole graph  

-----

<a name="Graph#hasVertex"></a>
#### *graph*.hasVertex(key) ⇒ <code>boolean</code>
Ask whether a vertex with a given key exists.


| Param | Type | Description |
| --- | --- | --- |
| key | <code>string</code> | the key to query |

**Returns**: <code>boolean</code> - whether there is a vertex with the given key  

-----

<a name="Graph#vertexValue"></a>
#### *graph*.vertexValue(key) ⇒ <code>\*</code>
Get the value associated with the vertex of a given key.


| Param | Type | Description |
| --- | --- | --- |
| key | <code>string</code> | the key to query |

**Returns**: <code>\*</code> - the value associated with the vertex of the given key.
Note that a return value of `undefined` can mean

1. that there is no such vertex, or
2. that the stored value is actually `undefined`.

Use [hasVertex](#Graph#hasVertex) to distinguish these cases.  

-----

<a name="Graph#addNewEdge"></a>
#### *graph*.addNewEdge(from, to, [value])
Add a new edge to this graph.


| Param | Type | Description |
| --- | --- | --- |
| from | <code>string</code> | the key for the originating vertex |
| to | <code>string</code> | the key for the terminating vertex |
| [value] | <code>\*</code> | the value to store in this new edge |

**Throws**:

- <code>[EdgeExistsError](#Graph.EdgeExistsError)</code> if an edge between `from` and `to` already exists
- <code>[VertexNotExistsError](#Graph.VertexNotExistsError)</code> if the `from` and/or `to` vertices do not yet exist in the graph


-----

<a name="Graph#createNewEdge"></a>
#### *graph*.createNewEdge(from, to, [value])
Add a new edge to this graph. If the `from` and/or `to` vertices do not yet exist
in the graph, they are implicitly added with an `undefined` value.


| Param | Type | Description |
| --- | --- | --- |
| from | <code>string</code> | the key for the originating vertex |
| to | <code>string</code> | the key for the terminating vertex |
| [value] | <code>\*</code> | the value to store in this new edge |

**Throws**:

- <code>[EdgeExistsError](#Graph.EdgeExistsError)</code> if an edge between `from` and `to` already exists


-----

<a name="Graph#setEdge"></a>
#### *graph*.setEdge(from, to, [value])
Set the value of an existing edge in this graph.


| Param | Type | Description |
| --- | --- | --- |
| from | <code>string</code> | the key for the originating vertex |
| to | <code>string</code> | the key for the terminating vertex |
| [value] | <code>\*</code> | the value to store in this edge |

**Throws**:

- <code>[EdgeNotExistsError](#Graph.EdgeNotExistsError)</code> if an edge between `from` and `to` does not yet exist


-----

<a name="Graph#spanEdge"></a>
#### *graph*.spanEdge(from, to, [value])
Make sure an edge between the `from` and `to` vertices in this graph.
If one already exists, nothing is done.
If one does not yet exist, a new edge is added with the given value.


| Param | Type | Description |
| --- | --- | --- |
| from | <code>string</code> | the key for the originating vertex |
| to | <code>string</code> | the key for the terminating vertex |
| [value] | <code>\*</code> | the value to store if a new edge is added |

**Throws**:

- <code>[VertexNotExistsError](#Graph.VertexNotExistsError)</code> if the `from` and/or `to` vertices do not yet exist in the graph


-----

<a name="Graph#addEdge"></a>
#### *graph*.addEdge(from, to, [value])
Add a new edge to this graph. If an edge between `from` and `to` already exists,
the value of that edge is overwritten.


| Param | Type | Description |
| --- | --- | --- |
| from | <code>string</code> | the key for the originating vertex |
| to | <code>string</code> | the key for the terminating vertex |
| [value] | <code>\*</code> | the value to store in this new edge |

**Throws**:

- <code>[VertexNotExistsError](#Graph.VertexNotExistsError)</code> if the `from` and/or `to` vertices do not yet exist in the graph


-----

<a name="Graph#ensureEdge"></a>
#### *graph*.ensureEdge(from, to, [value])
Make sure an edge between the `from` and `to` vertices exists in this graph.
If it already exists, nothing is done.
If it does not yet exist, a new edge is added with the given value.
If the `from` and/or `to` vertices do not yet exist
in the graph, they are implicitly added with an `undefined` value.


| Param | Type | Description |
| --- | --- | --- |
| from | <code>string</code> | the key for the originating vertex |
| to | <code>string</code> | the key for the terminating vertex |
| [value] | <code>\*</code> | the value to store if a new edge is added |


-----

<a name="Graph#createEdge"></a>
#### *graph*.createEdge(from, to, [value])
Add a new edge to this graph. If an edge between the `from` and `to`
vertices already exists, the value of that edge is overwritten.
If the `from` and/or `to` vertices do not yet exist
in the graph, they are implicitly added with an `undefined` value.


| Param | Type | Description |
| --- | --- | --- |
| from | <code>string</code> | the key for the originating vertex |
| to | <code>string</code> | the key for the terminating vertex |
| [value] | <code>\*</code> | the value to store if a new edge is added |


-----

<a name="Graph#removeExistingEdge"></a>
#### *graph*.removeExistingEdge(from, to)
Remove an existing edge from this graph.


| Param | Type | Description |
| --- | --- | --- |
| from | <code>string</code> | the key for the originating vertex |
| to | <code>string</code> | the key for the terminating vertex |

**Throws**:

- <code>[EdgeNotExistsError](#Graph.EdgeNotExistsError)</code> if an edge between the `from` and `to` vertices doesn't exist


-----

<a name="Graph#removeEdge"></a>
#### *graph*.removeEdge(from, to)
Remove an edge from this graph.
If an edge between the `from` and `to` vertices doesn't exist, nothing happens.


| Param | Type | Description |
| --- | --- | --- |
| from | <code>string</code> | the key for the originating vertex |
| to | <code>string</code> | the key for the terminating vertex |


-----

<a name="Graph#edgeCount"></a>
#### *graph*.edgeCount() ⇒ <code>number</code>
**Returns**: <code>number</code> - the number of edges in the whole graph  

-----

<a name="Graph#hasEdge"></a>
#### *graph*.hasEdge(from, to) ⇒ <code>boolean</code>
Ask whether an edge between given `from` and `to` vertices exist.


| Param | Type | Description |
| --- | --- | --- |
| from | <code>string</code> | the key for the originating vertex |
| to | <code>string</code> | the key for the terminating vertex |

**Returns**: <code>boolean</code> - whether there is an edge between the given `from` and `to` vertices  

-----

<a name="Graph#edgeValue"></a>
#### *graph*.edgeValue(from, to) ⇒ <code>\*</code>
Get the value associated with the edge between given `from` and `to` vertices.


| Param | Type | Description |
| --- | --- | --- |
| from | <code>string</code> | the key for the originating vertex |
| to | <code>string</code> | the key for the terminating vertex |

**Returns**: <code>\*</code> - the value associated with the edge between the given `from` and `to` vertices
Note that a return value of `undefined` can mean

1. that there is no such edge, or
2. that the stored value is actually `undefined`.

Use [hasEdge](#Graph#hasEdge) to distinguish these cases.  

-----

<a name="Graph#vertices"></a>
#### *graph*.vertices() ⇒ <code>Iterator.&lt;string, \*&gt;</code>
Iterate over all vertices of the graph, in no particular order.

**Returns**: <code>Iterator.&lt;string, \*&gt;</code> - an object conforming to the [ES6 iterator protocol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterator_protocol)  
**Example**  
```JavaScript
for (var it = graph.vertices(), keyVal = it.next(); !it.done;) {
    var key   = keyVal[0],
        value = keyVal[1];
    // iterates over all vertices of the graph
}
```
**Example**  
```JavaScript
// in ECMAScript 6, you can use a for..of loop
for (let [key, value] of graph.vertices()) {
    // iterates over all vertices of the graph
}
```
**See**: [@@iterator](#Graph#@@iterator)

-----

<a name="Graph#@@iterator"></a>
#### *graph*.@@iterator() ⇒ <code>Iterator.&lt;string, \*&gt;</code>
A [Graph](#Graph) object is itself [iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterable_protocol),
and serves as a short notation in ECMAScript 6 to iterate over all vertices in the graph, in no particular order.

**Returns**: <code>Iterator.&lt;string, \*&gt;</code> - an object conforming to the [ES6 iterator protocol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterator_protocol)  
**Example**  
```JavaScript
for (let [key, value] of graph) {
    // iterates over all vertices of the graph
}
```
**See**: [vertices](#Graph#vertices)

-----

<a name="Graph#edges"></a>
#### *graph*.edges() ⇒ <code>Iterator.&lt;string, string, \*&gt;</code>
Iterate over all edges of the graph, in no particular order.

**Returns**: <code>Iterator.&lt;string, string, \*&gt;</code> - an object conforming to the [ES6 iterator protocol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterator_protocol)  
**Example**  
```JavaScript
for (var it = graph.edges(), fromToVal = it.next(); !it.done;) {
    var from  = fromToVal[0],
        to    = fromToVal[1],
        value = fromToVal[2];
    // iterates over all edges of the graph
}
```
**Example**  
```JavaScript
// in ECMAScript 6, you can use a for..of loop
for (let [from, to, value] of graph.edges()) {
    // iterates over all vertices of the graph
}
```

-----

<a name="Graph#verticesFrom"></a>
#### *graph*.verticesFrom(from) ⇒ <code>Iterator.&lt;string, \*, \*&gt;</code>
Iterate over the outgoing edges of a given vertex in the graph, in no particular order.


| Param | Type | Description |
| --- | --- | --- |
| from | <code>string</code> | the key of the vertex to take the outgoing edges from |

**Throws**:

- <code>[VertexNotExistsError](#Graph.VertexNotExistsError)</code> if a vertex with the given `from` key does not exist

**Returns**: <code>Iterator.&lt;string, \*, \*&gt;</code> - an object conforming to the [ES6 iterator protocol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterator_protocol)  
**Example**  
```JavaScript
for (var it = graph.verticesFrom(from), toVertexEdge = it.next(); !it.done;) {
    var to          = toVertexEdge[0],
        vertexValue = toVertexEdge[1],
        edgeValue   = toVertexEdge[2];
    // iterates over all outgoing vertices of the `from` vertex
}
```
**Example**  
```JavaScript
// in ECMAScript 6, you can use a for..of loop
for (let [to, vertexValue, edgeValue] of graph.verticesFrom(from)) {
    // iterates over all outgoing edges of the `from` vertex
}
```

-----

<a name="Graph#verticesTo"></a>
#### *graph*.verticesTo(to) ⇒ <code>Iterator.&lt;string, \*, \*&gt;</code>
Iterate over the incoming edges of a given vertex in the graph, in no particular order.


| Param | Type | Description |
| --- | --- | --- |
| to | <code>string</code> | the key of the vertex to take the incoming edges from |

**Throws**:

- <code>[VertexNotExistsError](#Graph.VertexNotExistsError)</code> if a vertex with the given `to` key does not exist

**Returns**: <code>Iterator.&lt;string, \*, \*&gt;</code> - an object conforming to the [ES6 iterator protocol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterator_protocol)  
**Example**  
```JavaScript
for (var it = graph.verticesTo(to), fromVertexEdge = it.next(); !it.done;) {
    var from        = fromVertexEdge[0],
        vertexValue = fromVertexEdge[1],
        edgeValue   = fromVertexEdge[2];
    // iterates over all outgoing vertices of the `from` vertex
}
```
**Example**  
```JavaScript
// in ECMAScript 6, you can use a for..of loop
for (let [from, vertexValue, edgeValue] of graph.verticesTo(to)) {
    // iterates over all incoming edges of the `to` vertex
}
```

-----

<a name="Graph#verticesWithPathFrom"></a>
#### *graph*.verticesWithPathFrom(from) ⇒ <code>Iterator.&lt;string, \*&gt;</code>
Iterate over all vertices reachable from a given vertex in the graph, in no particular order.


| Param | Type | Description |
| --- | --- | --- |
| from | <code>string</code> | the key of the vertex to take the reachable vertices from |

**Throws**:

- <code>[VertexNotExistsError](#Graph.VertexNotExistsError)</code> if a vertex with the given `from` key does not exist

**Returns**: <code>Iterator.&lt;string, \*&gt;</code> - an object conforming to the [ES6 iterator protocol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterator_protocol)  
**Example**  
```JavaScript
for (var it = graph.verticesWithPathFrom(from), keyValue = it.next(); !it.done;) {
    var key   = keyValue[0],
        value = keyValue[1];
    // iterates over all vertices reachable from `from`
}
```
**Example**  
```JavaScript
// in ECMAScript 6, you can use a for..of loop
for (let [key, value] of graph.verticesWithPathFrom(from)) {
    // iterates over all vertices reachable from `from`
}
```

-----

<a name="Graph#verticesWithPathTo"></a>
#### *graph*.verticesWithPathTo(to) ⇒ <code>Iterator.&lt;string, \*&gt;</code>
Iterate over all vertices from which a given vertex in the graph can be reached, in no particular order.


| Param | Type | Description |
| --- | --- | --- |
| to | <code>string</code> | the key of the vertex to take the reachable vertices from |

**Throws**:

- <code>[VertexNotExistsError](#Graph.VertexNotExistsError)</code> if a vertex with the given `to` key does not exist

**Returns**: <code>Iterator.&lt;string, \*&gt;</code> - an object conforming to the [ES6 iterator protocol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterator_protocol)  
**Example**  
```JavaScript
for (var it = graph.verticesWithPathTo(to), keyValue = it.next(); !it.done;) {
    var key   = keyValue[0],
        value = keyValue[1];
    // iterates over all vertices from which `to` can be reached
}
```
**Example**  
```JavaScript
// in ECMAScript 6, you can use a for..of loop
for (let [key, value] of graph.verticesWithPathTo(to)) {
    // iterates over all vertices from which `to` can be reached
}
```

-----

<a name="Graph#vertices_topologically"></a>
#### *graph*.vertices_topologically() ⇒ <code>Iterator.&lt;string, \*&gt;</code>
Iterate over all vertices of the graph in topological order.

**Returns**: <code>Iterator.&lt;string, \*&gt;</code> - an object conforming to the [ES6 iterator protocol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterator_protocol)  
**Example**  
```JavaScript
for (var it = graph.vertices_topologically(), keyVal = it.next(); !it.done;) {
    var key   = keyVal[0],
        value = keyVal[1];
    // iterates over all vertices of the graph in topological order
}
```
**Example**  
```JavaScript
// in ECMAScript 6, you can use a for..of loop
for (let [key, value] of graph.vertices_topologically()) {
    // iterates over all vertices of the graph in topological order
}
```

-----

<a name="Graph#clearEdges"></a>
#### *graph*.clearEdges()
Remove all edges from the graph, but leave the vertices intact.


-----

<a name="Graph#clear"></a>
#### *graph*.clear()
Remove all edges and vertices from the graph, putting it back in its initial state.


-----

<a name="Graph#equals"></a>
#### *graph*.equals(other, [eq]) ⇒ <code>boolean</code>
Ask whether this graph and another graph are equal.
Two graphs are equal if they have the same vertices and the same edges.


| Param | Type | Description |
| --- | --- | --- |
| other | <code>[Graph](#Graph)</code> | the other graph to compare this one to |
| [eq] | <code>function</code> | a custom equality function for stored values; defaults to `===`     comparison; The first two arguments are the two values to compare.     If they are vertex values, the third argument is the vertex key.     If they are edge values, the third and fourth argument are the     `from` and `to` keys respectively. (So you can test the fourth     argument to distinguish the two cases.) |

**Returns**: <code>boolean</code> - `true` if the two graphs are equal; `false` otherwise  

-----

<a name="Graph#cycle"></a>
#### *graph*.cycle() ⇒ <code>array</code>
Find any directed cycle in this graph.

**Returns**: <code>array</code> - an array with the keys of a cycle in order;
                  `null`, if there is no cycle  

-----

<a name="Graph#hasCycle"></a>
#### *graph*.hasCycle() ⇒ <code>boolean</code>
Test whether this graph contains a directed cycle.

**Returns**: <code>boolean</code> - whether this graph contains a directed cycle  

-----

<a name="Graph#path"></a>
#### *graph*.path(from, to) ⇒ <code>array</code>
Find any path between a given pair of keys.


| Param | Type | Description |
| --- | --- | --- |
| from | <code>string</code> | the originating vertex |
| to | <code>string</code> | the terminating vertex |

**Returns**: <code>array</code> - an array with the keys of the path found between the two vertices,
                  including those two vertices themselves; `null` if no such path exists  

-----

<a name="Graph#hasPath"></a>
#### *graph*.hasPath(from, to) ⇒ <code>boolean</code>
Test whether there is a directed path between a given pair of keys.


| Param | Type | Description |
| --- | --- | --- |
| from | <code>string</code> | the originating vertex |
| to | <code>string</code> | the terminating vertex |

**Returns**: <code>boolean</code> - whether such a path exists  

-----

<a name="Graph#clone"></a>
#### *graph*.clone([tr]) ⇒ <code>[Graph](#Graph)</code>
Create a clone of this graph.


| Param | Type | Description |
| --- | --- | --- |
| [tr] | <code>function</code> | a custom transformation function for stored values; defaults to     the identity function; The first argument is the value to clone.     If it is a vertex value, the third argument is the vertex key.     If it is an edge value, the third and fourth argument are the     `from` and `to` keys respectively. (So you can test the fourth     argument to distinguish the two cases.) |

**Returns**: <code>[Graph](#Graph)</code> - a clone of this graph  

-----

<a name="Graph#transitiveReduction"></a>
#### *graph*.transitiveReduction([tr]) ⇒ <code>[Graph](#Graph)</code>
Create a clone of this graph, but without any transitive edges.


| Param | Type | Description |
| --- | --- | --- |
| [tr] | <code>function</code> | a custom transformation function for stored values; defaults to     the identity function; The first argument is the value to clone.     If it is a vertex value, the third argument is the vertex key.     If it is an edge value, the third and fourth argument are the     `from` and `to` keys respectively. (So you can test the fourth     argument to distinguish the two cases.) |

**Returns**: <code>[Graph](#Graph)</code> - a clone of this graph  

-----

<a name="Graph.VertexExistsError"></a>
#### *Graph*.VertexExistsError ⇐ <code>Error</code>
This type of error is thrown when specific vertices are expected not to exist, but do.

**Extends:** <code>Error</code>  

-----

<a name="Graph.VertexExistsError#vertices"></a>
##### *vertexExistsError*.vertices : <code>Set.&lt;{key: string, value}&gt;</code>
the set of relevant vertices


-----

<a name="Graph.VertexNotExistsError"></a>
#### *Graph*.VertexNotExistsError ⇐ <code>Error</code>
This type of error is thrown when specific vertices are expected to exist, but don't.

**Extends:** <code>Error</code>  

-----

<a name="Graph.VertexNotExistsError#vertices"></a>
##### *vertexNotExistsError*.vertices : <code>Set.&lt;{key: string}&gt;</code>
the set of relevant vertices


-----

<a name="Graph.EdgeExistsError"></a>
#### *Graph*.EdgeExistsError ⇐ <code>Error</code>
This type of error is thrown when specific edges are expected not to exist, but do.

**Extends:** <code>Error</code>  

-----

<a name="Graph.EdgeExistsError#edges"></a>
##### *edgeExistsError*.edges : <code>Set.&lt;{from: string, to: string, value}&gt;</code>
the set of relevant edges


-----

<a name="Graph.EdgeNotExistsError"></a>
#### *Graph*.EdgeNotExistsError ⇐ <code>Error</code>
This type of error is thrown when specific edges are expected to exist, but don't.

**Extends:** <code>Error</code>  

-----

<a name="Graph.EdgeNotExistsError#edges"></a>
##### *edgeNotExistsError*.edges : <code>Set.&lt;{from: string, to: string}&gt;</code>
the set of relevant edges


-----

<a name="Graph.HasConnectedEdgesError"></a>
#### *Graph*.HasConnectedEdgesError ⇐ <code>Error</code>
This type of error is thrown when a vertex is expected not to have connected edges, but does.

**Extends:** <code>Error</code>  

-----

<a name="Graph.HasConnectedEdgesError#key"></a>
##### *hasConnectedEdgesError*.key : <code>string</code>
the key of the relevant vertex


-----

<a name="Graph.CycleError"></a>
#### *Graph*.CycleError ⇐ <code>Error</code>
This type of error is thrown when a graph is expected not to have a directed cycle, but does.

**Extends:** <code>Error</code>  

-----

<a name="Graph.CycleError#cycle"></a>
##### *cycleError*.cycle : <code>Array.&lt;string&gt;</code>
the vertices involved in the cycle


-----

