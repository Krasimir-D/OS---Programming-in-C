# Зад. 82 2016-SE-01 Напишете програма на C, която приема параметър - име на (двоичен) файл с байтове. Програмата трябва да сортира файла.

**I decided to reverse the contents of the file as a "sorting" algo**

<p>

```c
#include <stdint.h>
#include <unistd.h>
#include <fcntl.h>
#include <err.h>
#include <stdlib.h>

int main(int argc, char* argv[]) {
	if (2 != argc)
		errx(1, "Invalid input. Path to file not provided");

	int fd = open(argv[1], O_RDONLY);
	if(-1 == fd)
		err(1, "open() for file %s failed", argv[1]);

	int fileSize = lseek(fd, 0, SEEK_END);
	uint8_t *fileContent = calloc(fileSize, sizeof(uint8_t));
	if (NULL == fileContent)
		err(1, "Can't allocate memory. Nothing more to do!");

	int newFileOffset = lseek(fd, 0, SEEK_SET);
	if (-1 == newFileOffset)
		err(1, "lseek() for file %s failed", argv[1]);
	
	int rc = 0;
	for (int i = 0; i < fileSize; ++i) {
		rc = read(fd, &fileContent[i], sizeof(uint8_t));
		if (-1 == rc)
			err(1, "read() for file %s failed", argv[1]);

		if (0 == rc)
			err(1, "Nothing more to read");
	}

	int fOutput = open("reversed.bin", O_WRONLY | O_CREAT | O_TRUNC, 0644);
	if (-1 == fOutput)
		err(1, "open() for output file failed");

	for (int i = fileSize - 1; i >= 0; --i) {
		rc = write(fOutput, &fileContent[i], sizeof(uint8_t));
		if (-1 == rc)
			 err(1, "write() for output file failed");
	}

	
	free(fileContent);

	if (-1 == close(fOutput))
		err(1, "close() for output file failed");

	if(-1 == close(fd))
		err(1, "close() for file %s failed", argv[1]);

	return 0;
}

```
</p>
