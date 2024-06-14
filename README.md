# random

## Building for bare metal target:  
By default Rust tries to build an executable that is able to run in your current system environment. For example, if you’re using Windows on x86_64, Rust tries to build an .exe Windows executable that uses x86_64 instructions. This environment is called your “host” system.

To describe different environments, Rust uses a string called target triple. You can see the target triple for your host system by running `rustc --version --verbose`:


```sh
rustc 1.35.0-nightly (474e7a648 2019-04-07)
binary: rustc
commit-hash: 474e7a6486758ea6fc761893b1a49cd9076fb0ab
commit-date: 2019-04-07
host: x86_64-unknown-linux-gnu
release: 1.35.0-nightly
LLVM version: 8.0
```

The above output is from a x86_64 Linux system. We see that the host triple is x86_64-unknown-linux-gnu, which includes the CPU architecture (x86_64), the vendor (unknown), the operating system (linux), and the ABI (gnu).

By compiling for our host triple, the Rust compiler and the linker assume that there is an underlying operating system such as Linux or Windows that uses the C runtime by default, which causes the linker errors. So, to avoid the linker errors, we can compile for a different environment with no underlying operating system.

An example of such a bare metal environment is the `thumbv7em-none-eabihf` target triple, which describes an embedded ARM system. The details are not important, all that matters is that the target triple has no underlying operating system, which is indicated by the none in the target triple. 

To build this binary, you need to compile for a bare metal target such as `thumbv7em-none-eabihf`:

- Command to download the bare metal target:  
```sh
rustup target add thumbv7em-none-eabihf
```  

- Build command:
```sh
cargo build --target thumbv7em-none-eabihf
```
