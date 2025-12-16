# Functions for error output

## err()
**Synopsis:**

#include <err.h>
void err(int eval, const char *fmt, ...);

The err() family of functions display a formatted error message on the standart error output. In all cases, the last component of the program name, a colon character, and a space are output.
If the *fmt* argument is not NULL, the printf-like formatted error message is output. The output is terminated by a newline character. Internally uses **errno**. Use **err()** when:

* a system call fails
* **errno** contains meaningful information

## errx()
**Synopsis:**

#include <err.h>
void errx(int eval, const char *fmt, ...);

The errx() function does essentially the same as **err()** in terms of outputting formatted error message. **errx()** ignores **errno**. Use **errx()** when:

* a logical/validation-related error occurs
* when **errno** is irrelevant or undefined

## As a rationale we can say that:
**errx()** is used for business-logic/program-logic type of errors.

**err()** is used for errors regarding failed system calls.
