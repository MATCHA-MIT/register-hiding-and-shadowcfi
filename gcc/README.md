# Register Hiding & ShadowCFI: Compiler patches

This folder contains the GCC patches which install a _Register Hide_ step before each indirect branch, and a _Register Restore_ step at each target of an indirect branch.
It also performs the optimization as described in §7.2 of the paper (_Global Register Hide_ and _Global Register Restore_).

## Build steps
1. Clone GCC:

```
git clone git://gcc.gnu.org/git/gcc.git
```

2. Checkout the commit on which the patches were tested (may work for other commits too):

```
cd gcc
git checkout 7adb7c6ea4cf3d7ea7867615a5a094c751715b14
```

3. Apply the patches:

```
git am ../gcc_registerhiding.patch
```

4. Download the prerequisites and configure:

```
./contrib/download_prerequisites
./configure --disable-multilib
````

5. Build the patches GCC:

```
make -j$(nproc)
```

6. Install GCC:

```
make install DESTDIR=$(pwd)/../gcc_registerhiding
```

Your installed GCC is located at `$(pwd)/../gcc_registerhiding/usr/local/bin/gcc`.
