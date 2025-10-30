## Submission Instructions
Submit your solution as a zip file containing the following files:
- All modified and new files from the xv6 directory.

---

## Task 0: Compiling and Running xv6
This section explains how to download, compile, and run the xv6 source code.

### Steps to Download and Compile xv6
1. **Open a Terminal**
   Open a shell or terminal in your virtual machine (e.g., bash shell).

2. **Navigate to the Desired Directory**
   Change your directory to the location where you want to download the xv6 source code:
   ```bash
   cd /projects/os
   ```

3. **Clone the xv6 Repository**
   Run the following command to clone the xv6 source code from the GitHub repository:
   ```bash
   git clone https://github.com/BGU-CS-OS/xv6-riscv.git
   ```

4. **Enter the Source Directory**
   ```bash
   cd xv6-riscv
   ```

5. **Build xv6**
   ```bash
   make
   ```

6. **Run xv6 in QEMU**
   ```bash
   make qemu
   ```

---

## Exercise Instructions
This exercise consists of two parts. **Part 2** is optional and worth **5 bonus points**. Carefully follow the instructions provided in the associated markdown files:

- [Part 1: System Call Implementation](#part-1-system-call-implementation)
- [Part 2: Bonus - Hello World Program](#part-2-bonus---hello-world-program)

---

## Part 1: System Call Implementation

### Overview
In this part, you will implement a new system call, `memsize`, in xv6. This system call will allow users to retrieve the current memory usage of a process. Follow these steps:

### Required Modifications

#### 1. **Modify `syscall.c`**
Add the following line to the list of external system calls:
```c
extern uint64 sys_memsize(void);
```
Then add the system call to the system call table:
```c
[SYS_memsize] sys_memsize,
```

#### 2. **Modify `syscall.h`**
Define the system call number for `memsize`:
```c
#define SYS_memsize 22
```

#### 3. **Modify `sysproc.c`**
Implement the `sys_memsize` function:
```c
uint64 sys_memsize(void) {
    return myproc()->sz;
}
```

#### 4. **Modify `user.h`**
Add the prototype for `memsize`:
```c
int memsize(void);
```

#### 5. **Modify `usys.pl`**
Add an entry for `memsize`:
```c
entry("memsize");
```

#### 6. **Modify `Makefile`**
Ensure that `memsize_test.c` is compiled by adding the following line:
```makefile
$U/_memsize_test\
```

#### 7. **Create `memsize_test.c`**
Write the following program to test the new system call:
```c
#include "kernel/types.h"
#include "user/user.h"
int main() {
    printf("I am using %d bytes.\n", memsize());
    char *boring = (char *)malloc(20000);
    printf("Now, I am using %d bytes.\n", memsize());
    free(boring);
    printf("Now after releasing memory, I am using %d bytes.\n", memsize());
    return 0;
}
```
#### 8. **Compile xv6**
Compile the entire xv6 system, including your new program, by running:
```bash
make qemu
```

#### 9. **Run the Program**
After starting xv6, execute your program by running the following command:
```bash
memsize_test
```

---

## Submission Checklist
Ensure the following files are included in your submission:

### Part 1:
- Modified files:
  - `syscall.c`
  - `syscall.h`
  - `sysproc.c`
  - `user.h`
  - `usys.pl`
  - `Makefile`
- New file:
  - `memsize_test.c`
  - `helloworld.c`

---

## Good Luck!
If you have any questions, feel free to reach out to the course staff.
