# Self-Reflection — Computer Organisation & Architecture (SECR1033)

---

## Lab 1 — Assembly Language Fundamentals

Working through the add/subtract programs was my first real hands-on contact with assembly. What surprised me most was how manually everything has to be done — moving values into specific registers, tracking exactly which register holds what. The debugging session (Part 2) using Watch, Registers, Autos, and Disassembly windows together was genuinely useful; seeing the byte-code representation of each instruction alongside the source made the link between high-level logic and machine execution much more concrete. I initially found the 8-bit vs 16-bit register distinction confusing (e.g. `AH` vs `AX` vs `EAX`), but running Part C cleared that up by forcing me to work with both sizes in the same program.

---

## Lab 2 — Arithmetic Equations & Operations

This lab pushed me to think carefully about how signed vs unsigned values behave in registers. The `NEG`, `MUL`, and `DIV` instructions each have implicit register conventions that are easy to get wrong — for instance, `MUL` always writes to `EDX:EAX`, and forgetting to clear `DX` before a `DIV` causes incorrect results. Working through Q2 (`Rval = (-Xval + (Yval – Zval)) + 1`) step by step in the debugger, and seeing `EAX` hold `FFFFFFDD` (two's complement for −35), made signed arithmetic much less abstract. The short notes I wrote for `MUL CX` and `DIV BL` helped me consolidate the rules in my own words, which I found more useful than just reading the textbook.

---

## Lab 3 — Link Libraries & Conditional Jumps

Combining Part 1 (LOOP/ADD for hexagon perimeter) and Part 2 (CMP/conditional jumps for array odd/even sums) into a single interactive menu program was the most challenging task across all three labs. Managing program flow with `CMP`, `JE`, `JNE`, `JG`, and `JMP` requires thinking about control flow very differently from high-level languages — there are no `if/else` blocks, just flags and jump targets. Getting the menu loop to restart cleanly (clear screen → main menu → branch → return) took several iterations. Drawing the flowchart first made the branch conditions much easier to translate into assembly.

---

## Group Project — CPU & Hardware Performance Benchmarks

My main takeaway from the benchmarking project is that **benchmark scores and real-world performance don't always align**. Computer A (Intel Core i7-1360P) scored highest on Geekbench multi-core (4289) and had the fastest disk throughput by far (sequential read ~2128 MB/s NVMe vs ~281 MB/s SATA on Computer C), yet in the assembly polynomial loop test, Computer A consistently had the *longest* CPU elapsed time across all loop counts. This result was counterintuitive and made me think more carefully about what each tool actually measures — Geekbench simulates varied workloads, while our assembly program is a tight single-threaded loop that is sensitive to clock speed, system load at the time of measurement, and background processes.

The project also showed me the value of using multiple tools together. CPU-Z gave static hardware specs, Geekbench gave standardised performance scores, Task Manager showed real-time resource consumption under different loads, and MiniTools revealed storage bottlenecks that the CPU benchmarks don't capture at all.

---

## Overall Reflection

Across the labs and project, the biggest shift in my thinking was learning to **reason at the hardware level**. Assembly removes all abstraction — there is no runtime, no garbage collector, no implicit type conversion. Every operation is explicit. This was frustrating at first but ultimately made me more aware of what happens underneath the code I write in higher-level languages. I also gained a more nuanced view of performance measurement: a single benchmark number rarely tells the whole story, and understanding *what* a tool measures is just as important as reading its output.
