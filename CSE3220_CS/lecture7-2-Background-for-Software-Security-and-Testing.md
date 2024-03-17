# Background for Software Security and Testing 

## 1. C
Softwares in C/C++ is necessary because
- it is performant
- it facilitates communication with or control of the hardware

A lot of languages, including safe languages still use components in C/C++

CPUs only understand binary
- Interpreter or just-in-time compiler frequently written in C/C++
- Libraries frequently written in C/C++
- Most commercial OSs are written in C/C++
- Most commercial VMs are written in C

### Java vs. C
Java
- Main goal: programmer productivity
- Widely used
- Rich ecosystem
- Platform independent
- Automatic memory management
- **Memory safety guaranteed**

C
- Main goal: performance and absolute control of resources
- Used mostly by system programmers
- Platform dependent
- Manual memory management
- **Memory safety not guaranteed**


## 2. Memory Errors
Memory errors are bugs in handling memory in memory unsafe languages
- A program accesses memory that it should not

### Stack Buffer Overflow
Occurs when a program writes to a memory address on the program's call stack outside of the intended data structure, which is usually a fixed-length buffer.