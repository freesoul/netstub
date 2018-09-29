
# Create C++ Stubs for .NET executables

## Motivation

[Simple Xtea Crypter](https://github.com/NateBrune/Simple-XTEA-Crypter) shows how to cypher a PE file with Xtea and running it from memory in a C++ compiled program. However, this did not appear to work for .NET executables.


## Steps with references

1. Grabbed and used [Simple Xtea Crypter](https://github.com/NateBrune/Simple-XTEA-Crypter) code to create a Xtea cyphered PE shellcode. You can simply "gcc xtea -o xtea.exe" it. Then you drag your .NET PE into it, and shellcode.h will appear.

Now, if you follow the steps described in that project with its runPE, it will just not work. Instead:


2. Grabbed, slightly modified, and used this code about [loading assembly code into a .NET environment with C++](https://www.codeproject.com/Articles/1236146/Protecting-NET-plus-Application-By-Cplusplus-Unman), and put the pieces together. Ah well, it did not work and I debugged to figure out that "SAFEARRAY *psaStaticMethodArgs = SafeArrayCreateVector(VT_VARIANT, 0, 0);" was creating wrong arguments for the .NET application (which in my case was a QuasaRAT executable, which expects some args in its Main). So I researched how to construct correctly these argv and argc (found it in a web which I do not remember) and included it.


3. Make sure you compile netstub.cpp with x86 or x64 depending on the .NET PE. Ah yes, and I used MVS 2017, this would not work with gcc.


Jean 09/2018
