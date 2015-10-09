### libbpf

This project offers a simple way to embed BPF in a cross-platform way for user-space applications.

Note that this is a niche project: generally, it's a much better idea to use the BPF 
functions provided by e.g. the Linux / BSD kernels.  The only time this is really useful is when
dealing with user-space networking stacks (e.g. DPDK).

Note that this is primarily a toy, not a production-ready implementation of BPF.

### Usage

The library includes two methods:

```C
    /** 
    Compiles a BPF program written in assembly-like syntax
    Code is first compiled into LLVM IR, then is either JIT'd or statically compiled
    depending on the options defined in the referenced 'prog' structure.
     
    For assembly syntax, see: https://www.kernel.org/doc/Documentation/networking/filter.txt
     
    @param text Program to compile
    @param prog Compiled program is written here
    @return zero on success and nonzero on failure
    */
    int libbpf_compile(bpf_program_t* prog, const char* text);
     
    /**
    Applies a compiled BPF program to something that is presumably a packet
     
    @param prog compiled BPF program to apply
    @param data contents of packet
    @param len size of packet
    @return value returned by BPF snippet
    */
    size_t libbpf_apply(const bpf_program_t* prog, const uint8_t* data, const size_t len);
```
