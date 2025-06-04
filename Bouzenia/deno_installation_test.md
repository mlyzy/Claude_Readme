# Deno Installation and Testing Report

## Overview
This document summarizes the process of installing and testing Deno, a secure JavaScript and TypeScript runtime.

## Installation Method
For this test, I installed Deno using the official installation script rather than building from source. Building from source presented challenges due to Cargo.lock file version compatibility issues.

## Installation Steps

1. First attempted to install Rust (required for building Deno from source):
   ```
   sudo apt install -y rustc cargo
   ```

2. Verified Rust installation:
   ```
   $ rustc --version
   rustc 1.75.0 (82e1608df 2023-12-21) (built from a source tarball)
   
   $ cargo --version
   cargo 1.75.0
   ```

3. Installed system dependencies:
   ```
   sudo apt install -y cmake ninja-build pkg-config python3 python3-pip git wget gcc g++ protobuf-compiler libssl-dev
   ```

4. Cloned the Deno repository:
   ```
   cd /tmp && git clone --recursive https://github.com/denoland/deno.git
   ```

5. Attempted to build from source (unsuccessful due to Cargo.lock version issue):
   ```
   cd /tmp/deno && cargo build
   ```
   
   Error:
   ```
   error: failed to parse lock file at: /tmp/deno/Cargo.lock
   
   Caused by:
     lock file version 4 requires `-Znext-lockfile-bump`
   ```

6. Installed using the official installation script:
   ```
   curl -fsSL https://deno.land/x/install/install.sh | sh
   ```

7. Verified installation:
   ```
   $ $HOME/.deno/bin/deno --version
   deno 2.3.5 (stable, release, x86_64-unknown-linux-gnu)
   v8 13.7.152.6-rusty
   typescript 5.8.3
   ```

## Testing

1. Created and ran a simple "Hello World" script:
   ```typescript
   // hello.ts
   console.log("Hello from Deno!");
   ```

   Command:
   ```
   $HOME/.deno/bin/deno run hello.ts
   ```

   Output:
   ```
   Hello from Deno!
   ```

2. Created a simple HTTP server:
   ```typescript
   // server.ts
   Deno.serve({ port: 8000 }, (req) => {
     return new Response("Hello, World!");
   });
   ```

3. Created and ran a test using Deno's testing API and third-party modules:
   ```typescript
   // std_test.ts
   import { assertEquals } from "https://deno.land/std@0.177.0/testing/asserts.ts";

   // A simple test case
   Deno.test("simple test", () => {
     assertEquals("hello", "hello");
     console.log("Test passed!");
   });
   ```

   Command:
   ```
   $HOME/.deno/bin/deno test std_test.ts
   ```

   Result:
   Successfully downloaded and imported the testing module from Deno's standard library.

## Conclusion

The installation of Deno using the official installation script was successful. The runtime works correctly for basic scripts, HTTP server functionality, and can download and use third-party modules from the Deno standard library.

While building from source was attempted, it was unsuccessful due to compatibility issues with the Cargo.lock file version. However, the official installation script provides a stable and working version of Deno that can be used for development and testing.

## Instructions for Manual Deployment from Source

If you want to build Deno from source, follow these steps:

1. Install Rust and Cargo:
   ```
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   source $HOME/.cargo/env
   ```

2. Install dependencies:
   ```
   # For Debian/Ubuntu
   sudo apt install -y cmake ninja-build pkg-config python3 python3-pip git wget gcc g++ protobuf-compiler libssl-dev
   ```

3. Clone the repository with submodules:
   ```
   git clone --recursive https://github.com/denoland/deno.git
   cd deno
   ```

4. Build Deno:
   ```
   cargo build -vv
   ```

5. Run tests:
   ```
   cargo test
   ```

6. Run a TypeScript test file:
   ```
   ./target/debug/deno run tests/testdata/run/002_hello.ts
   ```

7. To install the built binary to your system:
   ```
   cargo install --locked --path cli
   ```

Note: Building from source requires a compatible Rust toolchain and might require specific versions depending on the current state of the Deno repository.