# **Team Work Plan ⁠— FuncyPy (FP Language)**

#### Yannis Panagis - Sergey Chirkunov - Aimilios Hatzistamou - James Kim

Our team’s deliverable is a functional language called **FuncyPy**. It uses a simple syntax to make functional programming more accessible to developers coming from object oriented languages with minimal syntax like Python. In our design, we aim to utilize Python syntax in functional paradigm (partial-application, no loops, immutable types) to make FP more accessible to people coming from an OOP background. For sample code syntax please refer to the appendix. 

## Description

The project codebase is broken down into different modules following the structure below and tracked with Github for version control. All major functions are tested using automated test cases and property-based tests where possible.

- **Helper Module (Common)** | The helper module will include common type definitions and common helper functions that are used across modules, such as functions that convert between types, and printing functions for debugging.
- **Lexer Module (James)** **|** **Lexer: string -> List Tokens** | The lexer module will tokenize inputs into specific types to be evaluated by the parser into an Abstract Syntax Tree. The Tokens will include token types such as identifiers, keywords, sperators, operators, literals and comments. An extension goal for this module will be to abstain from using any .NET features or types such as the .NET floating-point type which is used by F# so that everything is FABLE compatible and it can port to other languages like JavaScript.
- **Parser Module (Yannis) |** **Parser: Token list** **-> Result** | The parser will initially be based on the more generic type parser (similar to Tick 3 extension) with parser combinators and will parse a stream of tokens from the lexer into an abstract syntax tree (see Pratt Parser extension).
- **Combinator Runtime System (Aimilios) |** **CombinatorRS: AstT -> ‘T** | The runtimes will evaluate expressions with arguments first, except for if-else conditionals which will evaluate condition-first. Input to the run-time will be the environment, with optionally the extended standard library as in extension below below. All functions will be Curried as lambdas, with memoization used throughout reduction (no function applied twice to same arguments).

- **Lambda Evaluation Runtime System (Sergey) |** **Module LambdaEvalRS: AstT -> ‘T** | Lambda body will be evaluated recursively. This requires: Dynamic name values, that can be resolved by holding the environment as a list of name-value pair. (i.e type list = item of name\*value | item\*list), and implementing closures such that all arguments are looked up and used. Finally the language should know when to evaluate. 

- **Main Module:** F# Modules cannot contain references to later defined values so including a ‘main module’ at the end of the pipeline will provide a frame to import all other modules and bring everything together.

## Extensions

We are proposing several possible extensions for our functional language. Which ones to pursue will be re-evaluated once further progress has been made with the code. All extensions will be completed in pairs because adding a few working extensions is a priority over adding many just for the sake of it.

- **Neater syntax:** Further syntax simplification by removing superfluous constructs such as ‘endif’ and adding constructs like ‘elif’.

- **Standard Library:** Built-in functions and modules, implemented in FuncyPy improve practical utility of the language. This includes functions like list functions such as Head, Tail, and isEmpty.

## Appendix

### **Syntax Demo for FuncyPy**

The following is an brief sample of the syntax of FuncyPy.

```F#
def tempFtoC Ftemp:
	p = Ftemp+32
	p*4/5.0
tempFtoC 32
```

## Build instructions

**Windows**

...to be added

"To be able to replicate the demo from the repo on a windows machine with a microsoft build, a single setup.bat file that pulls in dependences and allows build"

"If there are multiple deliverables - e.g. Expecto tests under dotnet and team deliverable under FABLE or dotnet - I expect the top-level README to have clear instructions for building and running each one, on a windows platform."

**Mac OSX**

To run tests in development mode, set RUN_TESTS in Program.fs to true and comment out the release code below. To run release code set RUN_TESTS to false.

**Team deliverable assessment: individual contributions**

1. **Aimilios**: Runtime improvements, system integration, parser-runtime Integration, CLI, standard lib, basic recursion, demo code
2. **Yannis**: Parser bug fixes and improvements, parser-lexer Integration, parser-runtime Integration, lexer unit tests, parser tests
3. **Sergey**: Arithmetic Operators Property-based Tests, Recursion (attempted)
4. **James**: Lexer bug fixes and improvements, lexer unit tests, Lexer 

Please see Individual README statements root of Master branch for more details on individual contributions during group phase.
