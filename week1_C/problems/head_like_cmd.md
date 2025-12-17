# Solution
Open a file and print the first 10 lines of its contents

<p>

```c
#include <unistd.h>
#include <fcntl.h>
#include <err.h>
#include <stdint.h>

#define ROWS 10

int main(int argc, char* argv[]) {
	if (argc != 2) {
		errx(1, "Invalid input! No path to file provided!");
	}
	

	int fd = open(argv[1], O_RDONLY);
	if (fd == -1) {
		err(1, "The provided path is invalid, no such file exists!");
	}

	char current;
	int rowsCnt = 0;
	int bytesRead = 0;
    int bytesWritten = 0;

	while(rowsCnt < ROWS) {
		bytesRead = read(fd, &current, 1);
        if (bytesRead == -1)
            err(1, "read() failed!");

		if (bytesRead == 0)
			errx(1, "EOF reached. Nothing more to read!");

        bytesWritten = write(1, &current, 1);
        if (bytesWritten == -1)
            err(1, "write() failed!");

		if (current == '\n')
			++rowsCnt;
	}

	if (close(fd)) {
        err(1, "close operation of fd=%d failed!", fd);
    }

	return 0;
}

```
</p>
