# System calls write/read open/close

## write from <unistd.h>
**write - write to a file descriptor**

**Synopsis:**

ssize_t write(int fd, const void* buf, size_t count);

write() writes up to *count* bytes from the buffer starting at *buf* to the file descriptor *fd*
The number of bytes written may be less than *count* if, for example, the size of the medium is insufficient or the system calls was interrupted.
On success the number of bytes written is returned. On error, -1 is returned and errno is set to indicate the error.

## read from <unistd.h>
**read - read from a file descriptor**

**Synopsis:**

ssize_t read(int fd, void* buf, size_t count);

read() attempts to read up to *count* bytes from a file descriptor *fd* into a buffer starting at *buf*.
On success the number of bytes read is returned. This size may be less than the requested amount *count*. This is not an error and my occurs to various reasons.
One such reason could be that the file simply does not contain *count* amount of bytes. On error, -1 is returned.

## open from <fcntl.h>
**open, creat - open and possibly create a file**

**Synopsis:**

int open(const char \*path, int flags, ...
                    /* mode_t mode */ );

int creat(const char \*path, mode_t mode);

The open() system call opens the file specified by *path*. If the file does not exist, it may optionally (if **O_CREAT** is specified in flags) be created by *open()*.
The return value of open() is a file descriptor, a small nonnegative integer that is an intex to an entry in the process's table of open file descriptors.

The argument *flags* must include one of the following access modes: **O_RDONLY, O_WRONLY, O_RDWR**. These request opening the file read-only, write-only, or read/write,
respectively.

In addition, zero or more file creation flags and file status flags can be bitwise ORed in *flags*. The file creation flags are **O_CLOEXEC, O_CREAT, O_DIRECTORY, O_EXCL, O_NOCTTY, O_NOFOLLOW,
O_TMPFILE, and O_TRUNC**.

## close from <unistd.h>
**close - close a file descriptor**

**Synopsis:**

int close(int fd);

close() closses a file descriptor, so that it no longer refers to any file and may be reused. Any record lock held on the file it was associated with, and owned by the process are removed.
close() returns zero on success. On error, -1 is returned.

## lseek from <unistd.h>
**lseek - reposition read/write file offset**

**Synopsis:**

off_t lseek(int fd, off_t offset, int whence);

**lseek()** repositions the file offset of the open file description associated with the file descriptor ***fd*** to argument ***offset*** according to the directive ***whence*** as it follows.

* **SEEK_SET** - reposition the file offset to ***offset*** bytes relative to the start of the file
* **SEEK_CUR** - reposition the file offset to ***offset*** bytes relative to the current file offset
* **SEEK_END** - reposition the file offset to ***offset*** bytes relative to the EOF

lseek() returns the resulting offset as measure in bytes from the beginning of the file. On error, the value (off_t) -1 is returned and errno is set to indicate the error
