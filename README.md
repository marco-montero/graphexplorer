# GraphExplorer

## Advanced interactive graph exploration/sandbox tool

### Goal

Create an interactive program (CLI, but extensible to GUI) where users build, modify, and query graphs using text-based
commands. Parsing is handle with Boost Spirit. The graph structure and algorithms are powered by Boost Graph.

---

### Why Boost Spirit and Boost Graph Are Excellent Candidates to Learn Advanced C++

### Boost Spirit

**Domain:** Parsing & Language Construction

#### Reasons to Learn

- **Template Metaprogramming Mastery:**  
  Spirit uses extensive template metaprogramming, exposing you to techniques like expression templates, compile-time grammar construction, and DSL (Domain Specific Language) design. It’s one of the best real-world examples of “writing code that writes code” in C++.
- **Modern C++ Idioms:**  
  Spirit leverages advanced C++ features: operator overloading, functors, template specialization, SFINAE (Substitution Failure Is Not An Error), and CRTP (Curiously Recurring Template Pattern).
- **Complex Abstractions:**  
  Understanding Spirit deepens your grasp of abstraction, generic programming, and how C++ supports embedded DSLs.
- **Practical Use Case:**  
  If you've ever wanted to write a parser or an interpreter (e.g., for configuration files, custom scripting languages, or data formats), Spirit lets you do so “the C++ way,” making it highly relevant.
- **Compile-Time Error Debugging:**  
  Using Spirit sharpens your skills in reading and debugging template-heavy compile-time errors, a must for high-performance, modern C++.
- **Impressive Expressiveness:**  
  Spirit demonstrates how expressive advanced C++ can be, rivaling languages like Haskell in certain domains.

### Boost Graph

**Domain:** Graph Data Structures & Algorithms

#### Reasons to Learn

- **Generic Programming:**  
  The Boost Graph Library (BGL) is a masterclass in generic programming. It abstracts graph algorithms and data structures so you can plug in your own types, container classes, and traits, a key advanced C++ skill.
- **Flexibility & Interoperability:**  
  BGL uses concepts and traits, allowing algorithms to work seamlessly across diverse user-defined graph types while maintaining performance.
- **Policy-Based Design:**  
  Learn how advanced C++ makes it possible to decouple algorithms from the underlying data structures, BGL’s “visitor” pattern is a powerful idiom.
- **Algorithm Complexity:**  
  It offers non-trivial algorithms (DFS, BFS, shortest paths, minimum spanning trees, etc.) and exposes you to both their theoretical aspects and practical C++ implementations.
- **Advanced Language Constructs:**  
  BGL leverages templates, template specialization, function objects, and advanced iterator and container design.
- **Industrial Relevance:**  
  Many real-world applications (network design, scheduling, bioinformatics) use graphs. Knowing BGL sets you up for modern C++ roles in these fields.
- **Working With Concepts:**  
  The library is ahead of its time in utilizing the concept paradigm (now formalized in C++20), so learning BGL is preparation for modern standard approaches.

---

## Tool details

### Sample Commands

- add node A
- add node B
- add edge A B
- add edge A B weight=3
- remove node A
- remove edge A B
- set node C color=red
- set edge A C weight=9
- shortest_path A D
- neighbors B
- degree A
- print
- help
- exit

### Key Functionalities

**1. Dynamic Graph Construction and Modification**
* Add/Remove Nodes/Edges:
  - Let users create and delete nodes and edges, optionally with attributes (label, weight, color, etc.).

**2. Query & Algorithms**
* Neighbors of a Node: List direct connections.
* Degree: Show in/out/mixed degree of a node.
* Shortest Path: Compute shortest paths (Dijkstra, BFS - configurable).
* Connectivity Checks: Are two nodes connected?
* Graph Traversal: BFS/DFS from a node - print sequence.

**3. Attribute Management**
* Properties: Allow users to set/read arbitrary node/edge properties (weight, color, etc.), stored as Boost Graph
 "bundled properties" or property maps.

**4. Persistence (Optional)**
* Save/Load: Allow users to export the graph description to a file and reload later (using your text language).

**5. Printing/Visualization**
* Print: Textual graph dump: list nodes, edges, and their properties.
* Export: Write graph to Graphviz DOT format for external visualization.

**Advanced & Optional Features**
* Undo/Redo: Maintain history of actions.
* Custom Algorithms: User-defined traversals, searches.
* Batch Commands: Parse and execute multi-line scripts.
* Predefined Graph Types: Load sample graphs (tress, cycles, etc.).

### Why it's interesting (C++ perspective)
* Boost Spirit: Design and implement a flexible command grammar, using semantic actions and ASTs.
* Boost Graph: Templated property-rich graph structures and algorithms.
* C++: Use variant, lambdas, perfect forwarding, and metaprogramming for extensibility.

### Details

**Node Commands**
* add node <name> [property1=value1 property2=value2 ...]
  - Add a node with optional properties.
* remove node <name>
  - Remove a node.
* rename node <oldname> <newname>
  - Rename a node.
* set node <name> <property>=<value> [property2=value2 ...]
  - Set/update properties.
* unset node <name> <property>
  - Remove property.
* show node <name>
  - Show all info/properties for a node.
* degree <name>
  - Show the degree (number of edges) for a node.
* neighbors <name>
  - List all neighbors (adjacent nodes).
* find node [property=value ...]
  - Find nodes matching property filters.
* list nodes
  - List all nodes.

**Edge Commands**
* add edge <src> <dst> [property1=value1 ...]
  - Add edge, optionally with properties (e.g., weight).
* remove edge <src> <dst>
  - Delete edge.
* set edge <src> <dst> <property>=<value> [property2=value2 ...]
  - Set/update properties.
* unset edge <src> <dst> <property>
  - Remove property.
* show edge <src> <dst>
  - Show edge info and properties.
* find edge [property=value ...]
   - Find edges matching properties.
* list edges
  - List all edges.

**Graph Structure and Queries**
* print
  - Print the current graph (nodes, edges, properties).
* clear
  - Erase the entire graph.

**Algorithms & Searches**
* shortest_path <src> <dst>
  - Find/print shortest path.
* path <src> <dst>
  - Find any path from src to dst.
* bfs <start>
  - Breadth-first traversal.
* dfs <start>
  - Depth-first traversal.
* connected <src> <dst>
  - Are two nodes connected?
* components
  - List connected components.
* mst
  - Minimum spanning tree (if weighted and undirected).
* cycle
  - Detect/report cycles.

**Properties & Graph Details**
* graph info
  - Print basic info: # nodes, # edges, directed/undirected, etc.
* set graph <property>=<value>
  - Set graph-wide property (e.g., mark as directed/undirected, defaults).
* list properties
  - List all node/edge properties in use.

**Persistence and I/O**
* save <filename>
  - Save graph (in your format, or Graphviz DOT).
* load <filename>
  - Load graph from file.
* export dot <filename>
  - Export as Graphviz DOT.
* import dot <filename>
  - Import Graphviz DOT (optional/advanced).

**Batch and Scripting**
* script <filename>
  - Execute command script from file.

**Help & Misc**
* help [command]
  - Show help about commands.
* exit or quit
  - Exit CLI.

**Command Syntax Legend**
* <> = required
* [] = optional
* property=value = property assignments (e.g. weight=3)

**Features to Consider**
* Undirected/Directed graph support (settable)
* Property data types (int, string, float, etc.)
* Attribute validation/typing
* Error handling (invalid nodes, duplicate additions, etc.)




