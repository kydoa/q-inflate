# q-inflate

[![Language](https://img.shields.io/badge/Language-C%2B%2B-00599C)](https://isocpp.org)
[![Status](https://img.shields.io/badge/Status-Ready%20for%20use-2ea043)](README.md)

Utilities for computing the expanded size of symbol-rewriting productions (rule-based reinflation). This repository contains two independent C++ implementations that parse production rule files and compute the total expanded length starting from the grammar root.

## Table of Contents

- [What This Project Does](#what-this-project-does)
- [Why This Project Is Useful](#why-this-project-is-useful)
- [Algorithm Overview](#algorithm-overview)
- [Getting Started](#getting-started)
- [Usage Examples](#usage-examples)
- [Project Structure](#project-structure)
- [Where To Get Help](#where-to-get-help)
- [Maintainers and Contributions](#maintainers-and-contributions)

## What This Project Does

This repository provides two programs that read production rules from text files and compute the expanded size of the grammar starting from its root symbol:

- `reinflador_hash` implemented in [src/hash.cpp](src/hash.cpp) — recursive memoized approach.
- `reinflador_fila` implemented in [src/fila.cpp](src/fila.cpp) — iterative, queue-based (topological) approach.

Each program expects the test cases to be present under the `casos_11` directory (text files). Output is printed to stdout in the form:

```
<path/to/testfile>
'<root_symbol>': <expanded_size>
==============
```

## Why This Project Is Useful

- Compare two algorithmic strategies for the same problem (memoized recursion vs. topological iteration).
- Study practical C++ code that uses the filesystem library, maps/sets, and timing utilities.
- Run and validate solutions against multiple test-case inputs in `casos_11`.

## Algorithm Overview

- `hash.cpp` — Builds production maps (`regras`) and computes expanded sizes with recursion + memoization. Efficient when many shared subtrees exist.
- `fila.cpp` — Builds dependency counts and processes symbols in topological order using a `std::queue`, computing sizes iteratively.
- Both implementations identify a root symbol as a left-hand-side that never appears on any right-hand-side.

Execution model:

1. Load rules from a `.txt` file into an internal map.
2. Identify the grammar root symbol.
3. Compute expanded size using the chosen algorithm.
4. Print results to stdout.

## Getting Started

### Prerequisites

- A C++17-compatible compiler (g++ or clang++)
- CMake (optional)

### Build with g++ (recommended quick start)

From the repository root run:

```bash
g++ -std=c++17 -O2 -o reinflador_hash src/hash.cpp
g++ -std=c++17 -O2 -o reinflador_fila src/fila.cpp
```

### Build with CMake (if you prefer)

The provided CMakeLists.txt expects a `src/main.cpp` target; if you want to use CMake, either add a small `main.cpp` that dispatches to one of the implementations or create a simple target. For quick experiments prefer the direct `g++` commands above.

## Usage Examples

1) Run the memoized implementation against all test files in `casos_11`:

```bash
./reinflador_hash
```

2) Run the queue-based implementation:

```bash
./reinflador_fila
```

Both programs walk `casos_11` and will print each test filename and the computed expanded size.

## Project Structure

```text
.
├── CMakeLists.txt
├── README.md
└── src/
	├── fila.cpp         # queue-based/topological implementation
	├── hash.cpp         # recursive memoized implementation
	└── casos_11/        # sample input test cases (.txt)
```

## Where To Get Help

- Start from the implementations: [src/hash.cpp](src/hash.cpp) and [src/fila.cpp](src/fila.cpp) for algorithm details.
- For build issues, check `CMakeLists.txt` or run the `g++` commands above.

## Maintainers

Maintainer:

- [@kydoa](https://github.com/kydoa)

