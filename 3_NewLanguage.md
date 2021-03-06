## Expectations, tips, features of a novel programming langauge
(please expand with reasoning)
- dependently typed
Dependent typing seems to bring together various good properties. First, it is the current top level construct that seems useful for representing 'real' computer programs operating on 'real' input data, rather than going into the more mathematical way of building types and proving relations about them. Second, it unifies compile- and runtime programming by making it possible for types to depend on values, at a certain level this means, macros become just ordinary, but well-typeable functions in the system and metaprogramming becomes ordinary programming (e.g. reflection).

- partial evaluation = staging ; binding time inference
Much flexibility and performance could be gained if at any point in a function, where a certain parameter becomes known (or its values are restricted such, that some code dependent on that restriction become dead) the function can be optimized into a specific version conatining less run-time operations.

- prop universe to guarantee type erasure
Some information about types, that are for example boolean judgements (is this type an Integral quantity, is this operation Commutative, etc.) must be validated and decided at compile-time, to maintain performance at runtime and/or signal errors at compile-time.

- whole program compilation
To make a detailed analysis and well supported decisions of rewrites throughout the program, the compiler must have as much information as possible about the problem at hand. Most compilers today trade thoroughness and modularity with compilation speed, with no option to give more time and resources for the compiler to analyze more. There should be a way to do this. Modularity should not stop the flow of useful information across module boundaries.

- aligment ; experimental
- control over memory layout
Layout in memory requires extensive care in context of performance tuning, especially with alignment. When creating parametric functionality, the developer has to have detailed control over how the alignment and padding of different types in composeite types (like elements of a tuple or record). While expliciteness would be too verbose, much of this information should be automatically inferred, or given at the type definition or combined from the environment. Memory layout should be precisely well-defined in all cases, otherwise it would create trouble when sharing structures between devices (like CPU-GPU sharing).

- no GC or optional
The control over the allocated memory should be in the hands of the programmer, because many real world problems are memory limited, and it is a complicated problem dependent task to fit every necessary data into the operational memory, especially, whan parts of it are dynamically re-allocated. Also, the point when GC kicks in could cause unplannable performance hits on runtime, causeing e.g. unexpectedly long frame time, or similar phenomena. 


## Design considerations:

1.: Static GC based on ASAP (see readings.md).
This analysis could insert memory deallocation based on analysis of heap structure, scoping etc. It still keeps GC, but also the runtime cost of that is reduced.

Fusing and reuse is not implemented in that document, but seems possible.


2.: Pointers, mutability, interior refernces:
Only two is possible out of this three at the same time.
We stick with immutability.


3: Modules, records, objects:

Agda modules seems to be a good starting point, but we need a clear summary on their limitations, we may need more to cover the use-case of prgama driven code specialsation like C/C++. Same with records.

At the widest scope, we may want to specialise a module or record programmatically, cluding all its contents (nested types, constants, functions, etc.). We need use-cases on this.


4.: Recursion:
Do we need a separate primitive or not?

Detecting multiple nested recursions between n functions and generating efficient code from that is hard.
Question: how frequent are these in real code?
Tail Call Elmination could solve some part of the issue, but we need use-cases and summary of the limitations of TCE.

Otherwise we may introduce special contructs.

5.: Impure functions: IO and random generators
Effect system might be needed, like PureScript.
If it is annotations like and not dependent, we could include it. Otherwise, annotation is needed from the programmer. There could be other complications, when effectful functions are composed between other effectful or non-effectful functions: when does the side effect triggers? Do we need polymorphism for this to avoid syntactic noise?

6. Compilation types:
Fast: interpreter like - simple memory representation
Slow: costy full analysis + ASAP analised representation

We may want to be able to change between the two at runtime, start with the fast, gradually change to the other as it becomes available. Goal: minimize development cycle. Final version always should be the full analysis version.

#### Note/question by Máté:

Is this really necessary? There are two ways that can mitigate this issue without having to jump through flaming hoops.

- Tooling tends to shift toward favoring build servers vs. traditional one-shot build systems. (The name renders it google-immune, build service would've been a better choice, hence I'll call it that.) A build server is a constantly running process, which when thought of very simply, keeps invoking `make` behind the background. Smarter build servers are instructed by the IDE, when certain files are edited, they trigger events in the build service which can invoke incremental builds with surgical precision. Modern build systems like meson and buck also insepct the contents and outcome of files and don't rebuild when not necessary.
  - Writing a comment inside the code has no impact on the binary, and even though timestamps of the output changes, building of depending files will not trigger.
  - Similarily, updating the private interface of a file does not change the exported symbols, so no re-linking is required.
  - These checks can be accelerated by hasing output binary files behind the scenes, buildling symbol tables, etc. Many things that can be done while the code is being edited, so builds will be faster.
- Optimizing the back-end for compilation speed. HSA uses an IR format that is very fast to compile for target back-ends (O(ms)), which is done on every application start. The HSA runtime is free to implement any caching mechanism it sees fit, but a few milliseconds delay "JIT"-ing HSAIL to binary is affordable.

I would argue that for the sake of reducing the time of the Edit-Build-Debug cycle, implementing a tricky on-the-fly migration of binary or even data layout is simply not worth it. I would sooner advocate for a well designed compilation model (something that has been layed out well) and write tooling accordingly. I would gladly engage in this part of the project.

#### Reply to Máté:
Optimization and runtime editing are two different aspects. The mentioned memory transition is simply an optimization pass at runtime, it is not related to runtime editing of the code. Editing is difficult as someone needs to prove the invariance of the change.


7. Decision related to dependent typing:
We monomoprhise from the dependently typed representation to the internal language, this way there should be no polymorphism left. This affects the memory layout: the user cannot represent simple dependent code: like reading variable length data at runtime. Does Introducing a variable length array type enough to cover the affected practical cases? What are the limitations, trade-offs?



## Things to discuss
- Indirect access: pointers / references how?
  Only 2 can be chosen of the following three: sharing, mutation, interior pointers] 
  
  ![Choose at most two](ChooseTwo.svg)

- Scoping, modules, objects
- Pure, impure, semi-pure functions and closures (important example: random number generators and I/O)
- Declarative compiler stage definitions via recursion schemes
- User defined stages / rewrite rules?
- high level vs low level GPU API
  - high level: *accelerate, futhark* ; **automagically works (or not)** (depends on fusion implicitly)
  - low level: *obsidian, [Functional Compute Language](https://github.com/dybber/fcl/blob/master/publications/fhpc2016-fcl.pdf)* ; **explicit user control**
  
 - Frontend syntax (curlybraced imperative-like, functional Haskell like)
 - Domain model for GPU concepts (primitive types and functions)
 - Nodegraph editing: what would be the good representation and mechanism for node based editing of a functional language?
 - Node edig tech: nodejs + yarn + ..., server side rendering and streaming...
  
## Current design of the compiler:

* Frontend - Dependently typed language, exressive, lots of information implicit

Elaboration: Frontend -> Core
- Desugaring
- Implicit -> Explicit
- Type inference
- Type checking
- Name resolution / scope checking
- Binding time analysis
	
* Core language - Dependently typed language with less elements, no memory layout info, everything is explicit

Transformations: Core to Core
- Memory layout analysis
- Partial evaluation
- Optimalization passes

Core -> Backend transformation
- Erasure (Eliminating polymorph type arguments from indexed types, like props)
          and / or Monomorfization: partial application on all type applications, again, polymorphism will be eliminated. Conversion of Pi types into simple functions (arrows): (eval Pi)
- Prop analysis		
- Closure conversion
- Lambda lifting
- Defunctionalization (generate eval/apply because of strictness)

* Backend - low level, Grin: LLVM like type system + sumtype, First order, strict, monomorf, immutable, SSA
	Short circuit: the interpreter like output exits here

Grin Transformation: Grin -> Grin
- ASAP heap / GRIN Heap hoisture analysis
- Full program analysis
- GRIN optimalisations: like case branch analysis, ...

- Grin handling of FFI: treats them as builtins.
	
final: GRIN -> LLVM

* LLVM

## Plans on the implementation of the frontend type checker
In parens the expected difficulty of implementation
- Dependent core (1)
- Prop (?)
- Type inference (6)
- Inductive data (15)
-- Dependent pattern match
- Modules, Namespacing
-- Simple (3)
-- More usable (10)
- Partial Application and Evaluation (?)
-- Binding time analysis

# Random observations

Type-in-Type plus Prop allows memory safety to be violated:

 1. Girard's paradox normally only allows one to construct an infinitely-looping term, invalidating the type system's consistency-as-a-logic (every type is inhabited), but not violating type safety / memory safety (no UB).
 
 2. But if we use Girard's paradox to prove something in Prop, then the proof is not evaluated (which would loop), but is instead erased, so we can create false assumptions and use them.
 
 3. So we can falsely prove e.g. that an index is in-bounds of an array when it isn't, and access arbitrary memory at runtime.
 
As long as the goal is only to protect against programmer mistakes, and not against dedicated attackers looking for exploits, this shouldn't be a huge problem (it is hard to write Girard's paradox on purpose, let alone by accident).
