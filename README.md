# **Mini Compiler – Complete Implementation**

A full-featured educational compiler implementation that demonstrates **all six classical phases of compilation**, built entirely from scratch **without parser generators**.
Ideal for academic projects, compiler design courses, and anyone learning how compilers work internally.


## 📋 **Features**

### **Supported Language Constructs**

* **Data Types:** `int`, `float`, `char`
* **Control Flow:** `if`, `elif`, `else`
* **Loops:** `while`, `for`
* **Functions:** declarations, recursion, parameter passing, return values
* **I/O:** `print`, `input`
* **Operators:**

  * Arithmetic: `+`, `-`, `*`, `/`, `%`
  * Relational: `==`, `!=`, `<`, `>`, `<=`, `>=`
  * Logical: `&&`, `||`, `!`
* **Nested Structures:** full support for nested blocks and scopes


## 🛠️ **Compiler Phases**

### **Phase 1: Lexical Analysis**

* Character-by-character tokenization
* Keyword recognition
* Number parsing (int & float)
* Char literal handling
* Comment support (`//`)
* Robust error detection

### **Phase 2: Syntax Analysis (Parsing)**

* Recursive descent parser (top-down)
* Abstract Syntax Tree (AST) creation
* Grammar-driven parsing
* Error recovery mechanisms

### **Phase 3: Semantic Analysis**

* Type checking with coercion
* Stack-based scope management
* Declaration-before-use validation
* Symbol table construction
* Initialization tracking

### **Phase 4: Intermediate Code Generation**

* Three-Address Code (TAC) output
* Label & jump management
* Temporary variable allocation

### **Phase 5: Optimization**

* Constant folding (`3 + 5 → 8`)
* Algebraic simplification (`x * 1 → x`)
* Dead code elimination

### **Phase 6: Code Generation**

* Pseudo-assembly generation
* Stack-based architecture
* Organized text & data sections

---

## 🚀 **Usage**

### **Command-Line**

```bash
# Compile a source file
python compiler.py test_program1.txt

# Interactive mode
python compiler.py --interactive
```

### **Programmatic Usage**

```python
from compiler import Compiler

compiler = Compiler()
success, result = compiler.compile(source_code, verbose=True)

if success:
    print("Compilation successful!")
    result['symbol_table'].print_table()
```

---

## 📁 **Project Structure**

```
mini-compiler/
├── grammar.txt              # Formal grammar specification
├── lexer.py                 # Phase 1: Lexical Analyzer
├── ast_nodes.py             # AST node definitions
├── parser.py                # Phase 2: Syntax Analyzer
├── symbol_table.py          # Symbol table manager
├── semantic_analyzer.py     # Phase 3: Semantic Analyzer
├── icg.py                   # Phase 4: Intermediate Code Generator
├── optimizer.py             # Phase 5: Code Optimizer
├── code_generator.py        # Phase 6: Final Code Generator
├── error_handler.py         # Centralized error handling
├── compiler.py              # Main compiler controller
├── test_program1.txt        # Test: Basic arithmetic
├── test_program2.txt        # Test: If-elif-else
├── test_program3.txt        # Test: Loops
├── test_program4.txt        # Test: Nested structures
├── test_errors.txt          # Test: Error detection
└── README.md
```

---

## 📖 **Grammar**

The full grammar specification (BNF format) is available in **grammar.txt**.

---

## 🔢 **Type Coercion Rules**

| Expression         | Result                |
| ------------------ | --------------------- |
| int + int          | int                   |
| float + float      | float                 |
| int + float        | float (int promoted)  |
| char in arithmetic | promoted to int       |
| int = float        | ❌ Error (narrowing)   |
| float = int        | ✔️ Allowed (widening) |

---

## 🧪 **Test Programs**

### **Test 1: Basic Arithmetic**

```c
int x;
x = 10 + 5 * 2;
print x;
```

### **Test 2: Control Flow**

```c
int score;
score = 85;

if (score >= 90) {
    print 1;
} elif (score >= 80) {
    print 2;
} else {
    print 0;
}
```

### **Test 3: Loops (Modern Syntax)**

```c
int sum;
sum = 0;

loop from i = 1 to 10 {
    sum = sum + i;
}
print sum;
```

### **Test 4: Functions (NEW!)**

```c
func int factorial(int n) {
    if (n <= 1) {
        return 1;
    }
    int temp;
    temp = n - 1;
    return n * factorial(temp);
}

int result;
result = factorial(5);
print result;  // Output: 120
```

---

## 🔍 **Error Handling**

The compiler identifies:

### **1. Lexical Errors**

* Unknown characters
* Malformed literals
* Invalid tokens

### **2. Syntax Errors**

* Missing semicolons
* Unmatched braces
* Invalid sequences

### **3. Semantic Errors**

* Undeclared variables
* Type mismatches
* Use-before-initialization
* Redeclaration in the same scope

---

## 📊 **Generated Output Files**

Given a file like `program.txt`, the compiler generates:

* `program.tac` — Three-Address Code
* `program_opt.tac` — Optimized TAC
* `program.asm` — Final assembly

---

## 🎓 **Educational Value**

This project helps learners understand:

* Full compiler architecture
* Lexing, parsing, semantic analysis
* AST design
* Intermediate code generation
* Optimization techniques
* Code generation for stack machines

Perfect for **semester projects, viva preparation, and demonstrations**.

---

## 🛠️ **Implementation Details**

### **Parser Choice: Recursive Descent**

Reasons:

* Easier manual implementation
* Better error messages
* Intuitive for small languages
* No complex table generation
* Ideal for teaching

### **Symbol Table Structure**

Stack-based nested scopes:

```txt
scopes = [
    {'x': SymbolEntry(...)},  # Global
    {'y': SymbolEntry(...)},  # Inner scope
]
```

### **Three-Address Code Format**

```
t0 = a + b
t1 = t0 * c
x = t1
IF_FALSE t2 GOTO L1
L1:
```

### **Example Compilation**

#### **Input**

```c
int x;
x = 5 + 3;
print x;
```

#### **Tokens**

```
INT, IDENTIFIER(x), SEMICOLON,
IDENTIFIER(x), ASSIGN,
INTEGER_LITERAL(5), PLUS, INTEGER_LITERAL(3), SEMICOLON, ...
```

#### **TAC**

```
ALLOC x int
t0 = 5 + 3
x = t0
PRINT x
```

#### **Optimized TAC**

```
ALLOC x int
x = 8
PRINT x
```

#### **Assembly**

```
x: .space 4  ; int
LOAD_IMM 8
STORE x
LOAD x
PRINT
```

---

## 🤝 **Contributing**

This project welcomes improvements to:

* Optimizations
* Language features
* Error diagnostics
* Test suite

---

## 📄 **License**

Free to use for educational and academic purposes.

---

## 👨‍💻 **Author**

Developed as a complete semester project demonstrating **all phases of compilation**.

---

**Happy Compiling! 🎉**

