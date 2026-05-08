Step 1: Add Inode Type
File: fs.h
#define T_SYMLINK 4
Extends inode types for symlink support
Step 2: Update stat.h
Add T_SYMLINK definition
Ensures consistency across system
Optional but recommended
Step 3: Add Syscall Number
File: syscall.h
#define SYS_symlink 22
Assign next available syscall number
Step 4: Add User API
File: user.h
int symlink(const char *target, const char *linkpath);
Exposes syscall to user programs
Step 5: Add Syscall Stub
File: usys.S
SYSCALL(symlink)
Connects user call to kernel
Step 6: Register Syscall
File: syscall.c
extern int sys_symlink(void);
Add to syscall table
Step 7: Implement sys_symlink
File: sysfile.c
Use create() with T_SYMLINK
Write target path with writei()
Step 8: Modify sys_open()
Detect T_SYMLINK
Read target using readi()
Resolve using namei()
Step 9: Add Test Program
Create testsymlink.c
Verify read via symlink
Test cycle detection
Step 10: Update Makefile
Add _testsymlink to UPROGS
Rebuild xv6
Run tests in QEMU