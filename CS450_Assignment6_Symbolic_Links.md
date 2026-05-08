CS450 – Assignment 6: Symbolic Links (xv6-public x86)
Deliverable: add symlink support: new inode type, syscall, and link resolution
Work type: individual
Target: MIT xv6-public (x86)
Points: 100
1. Objectives
Extend xv6 inode types and file system behavior safely
Add a syscall with correct on-disk metadata writing
Modify path/open resolution to follow links with loop prevention
2. Specification
2.1 New Inode Type
#define T_SYMLINK 4
The location depends on your base (fs.h / stat.h).
A symlink inode stores its target path string in its data blocks (NUL-terminated; truncate safely).
2.2 Syscall
int symlink(const char *target, const char *linkpath);
Behavior:
Create linkpath as inode type T_SYMLINK
Write target into the inode’s data blocks
Return 0 on success, -1 on error
2.3 Resolution
When opening a path:
If the inode is a symlink, read its target and continue lookup
Support chained symbolic links
Enforce a maximum depth (e.g., 10) to prevent cycles
3. Starter Test
Use testsymlink.c. It must verify:
Reading through a symlink returns the target’s contents
A cycle triggers failure due to the depth limit
4. Grading
Correct symlink creation and persistence: 30
Correct resolution and depth limit: 40
Tests and write-up: 30