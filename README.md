# Vs Extension
- [CPH](https://marketplace.visualstudio.com/items?itemName=DivyanshuAgrawal.competitive-programming-helper)

# Installing GCC/G++ on macOS

This guide explains how to install the GNU C and C++ compilers (`gcc` and `g++`) on macOS using Homebrew.

## Prerequisites

Before installing GCC, make sure you have:

- A Mac running macOS
- An internet connection
- Administrator privileges (you may be prompted for your password during installation)

---

## Step 1: Install Homebrew

Homebrew is the most popular package manager for macOS and is required to install GCC.

Open **Terminal** and run:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

---

## Step 2: Configure Homebrew

After the installation finishes, Homebrew may display the following instructions:

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

These commands:

1. Add Homebrew to your shell configuration file (`~/.zprofile`).
2. Load Homebrew into your current terminal session immediately.

> **Note:** On Apple Silicon Macs (M1, M2, M3, etc.), Homebrew is installed in `/opt/homebrew`. These commands ensure that the `brew` command is available every time you open a new terminal.

Verify that Homebrew is installed correctly:

```bash
brew --version
```

You should see output similar to:

```text
Homebrew 4.x.x
```

---

## Step 3: Install GCC

Install the GNU Compiler Collection:

```bash
brew install gcc
```

Homebrew installs GCC with versioned executable names to avoid conflicts with Apple's default Clang compiler.

For example, after installation, you may see:

```text
gcc-16
g++-16
```

where `16` is the installed GCC version.

---

## Step 4: Find the Installed GCC Version

List the installed GCC executables:

```bash
ls /opt/homebrew/bin/gcc-* /opt/homebrew/bin/g++-*
```

Alternatively, you can run:

```bash
brew info gcc
```

Example output:

```text
/opt/homebrew/bin/gcc-16
/opt/homebrew/bin/g++-16
```

---

## Step 5: Create Convenient `gcc` and `g++` Commands

By default, you need to type:

```bash
gcc-16
g++-16
```

To use the simpler commands `gcc` and `g++`, create symbolic links.

Navigate to Homebrew's binary directory:

```bash
cd /opt/homebrew/bin/
```

Create the symbolic links:

```bash
ln -s gcc-{version} gcc
ln -s g++-{version} g++
```

Replace `{version}` with your installed GCC version.

For example:

```bash
ln -s gcc-16 gcc
ln -s g++-16 g++
```

> **Note:** If `gcc` or `g++` links already exist, remove them first:

```bash
rm gcc g++
ln -s gcc-16 gcc
ln -s g++-16 g++
```

---

## Step 6: Verify the Installation

### Refresh Your Shell

After creating the symbolic links, refresh your shell so that the new `gcc` and `g++` commands are recognized immediately:

```bash
hash -r
rehash
exec zsh
```

- `hash -r` clears Bash's command cache.
- `rehash` refreshes Zsh's command cache.
- `exec zsh` starts a new Zsh session and reloads your shell environment.

You can now verify that the commands are available:

```bash
which gcc
which g++
gcc --version
g++ --version
```

Example output:

```text
gcc (Homebrew GCC 16.x.x) 16.x.x
g++ (Homebrew GCC 16.x.x) 16.x.x
```

---

## Compiling a C Program

Create a file named `hello.c`:

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

Compile and run:

```bash
gcc hello.c -o hello
./hello
```

Output:

```text
Hello, World!
```

---

## Compiling a C++ Program

Create a file named `hello.cpp`:

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```

Compile and run:

```bash
g++ hello.cpp -o hello
./hello
```

Output:

```text
Hello, World!
```

---

## Quick Installation Commands

```bash
# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Configure Homebrew
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

# Install GCC
brew install gcc

# Create convenient gcc and g++ commands
cd /opt/homebrew/bin/
ln -s gcc-{version} gcc
ln -s g++-{version} g++
```

---

## Notes

- Apple ships with the Clang compiler by default. Installing GCC does **not** remove Clang.
- Homebrew installs GCC using versioned executable names (`gcc-15`, `g++-15`, etc.) to avoid conflicts.
- If you upgrade GCC to a newer major version, update the symbolic links to point to the new version.
- The installation path `/opt/homebrew` applies to Apple Silicon Macs (M1, M2, M3, M4, M5 etc.). On Intel Macs, Homebrew is typically installed in `/usr/local`.

- ---

## References

- [Homebrew Official Website](https://brew.sh)

- [Homebrew Installation Documentation](https://docs.brew.sh/Installation)

- [GCC (GNU Compiler Collection)](https://gcc.gnu.org/)
