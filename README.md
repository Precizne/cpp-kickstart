# cpp-kickstart

A modern C++26 starter template for system development, HFT, and competitive programming.

## 🧰 Toolchain Overview

| Component          | Tool                      |
|--------------------|---------------------------|
| Compiler           | `clang++`                 |
| Linker             | `lld`                     |
| Debugger           | `lldb`                    |
| Dependency Manager         | `conan`                   |
| Build Generator       | `cmake`         |
| Build System           | `ninja`                   |
| Cache              | `ccache`                  |
| Formatter          | `clang-format`            |
| Static Analysis    | `clang-tidy`, `cpplint`   |
| Runtime Checks             | `sanitizers`              |
| Profiler           | `valgrind`, `perf`        |
| Standard Library   | `libstdc++`               |
| Language Standard  | `C++26`                   |

## 📦 Dependencies (via Conan)

```cmake
[requires]
<library-name>/<version>

[generators]
CMakeToolchain
CMakeDeps
```

## 🛠 Build & Run

```bash
# 1. Detect or refresh your Conan profile
conan profile detect --force

# 2. Install dependencies
conan install . --output-folder=build --build=missing --profile=default

# 3.1 Configure the project (Debug build with sanitizers)
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug

# 3.2 Configure the project (Release build without sanitizers)
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DUSE_SANITIZERS=OFF

# 4. Build with Ninja
cmake --build build -j

# 5. Run
./build/main
```

## 🧪 Runtime Debugging with `valgrind`

```bash
valgrind --leak-check=full ./build/main
```

## 🔥 Performance Profiling with `perf`

### 🚀 Basic Usage

#### 🔬 CPU Event Summary

```bash
perf stat ./build/main
```

#### 🧪 Function Hotspot Profiling

```bash
perf record ./build/main
perf report
```

#### 📈 Call Graph Analysis

```bash
perf record -g ./build/main
perf report --call-graph
```

#### 🔥 Real-Time System Profiling

```bash
sudo perf top
```

#### 💡 Flame-graphs

```bash
perf record -g ./build/main
perf script > out.perf
./stackcollapse-perf.pl out.perf | ./flamegraph.pl > flamegraph.svg
```
