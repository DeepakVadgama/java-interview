## Importance of Compile Time vs JIT

- In compile - code is converted directly to architecture (machine language). Example: Go
- In JIT - code is converted at runtime, just before 
- Advantage: it can check availability of resources (RAM, CPU etc) and decide on corresponding optimizations 
- Advantage: it can keep running for a while a find hot snippets of code, and optimize them even further. Eg: Android 7
