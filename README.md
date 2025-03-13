# get_next_line

<p align="center">
  <img src="https://raw.githubusercontent.com/ayogun/42-project-badges/refs/heads/main/covers/cover-get_next_line.png" alt="get_next_line Cover">
</p>
<img src="https://img.shields.io/badge/Score-125%2F100-brightgreen" alt="Score Badge">

A function that reads and returns a line from a file descriptor, developed as part of the 42 curriculum.  
**`get_next_line`** handles reading text files or standard input line by line, even across multiple file descriptors.

---

## Features
- Reads a line from a given file descriptor, including the trailing newline (`\n`)  
- Manages reading through large files or standard input efficiently  
- Works with any `BUFFER_SIZE` defined at compile time  
- Properly frees memory to avoid leaks  
- **Bonus:** Handles multiple file descriptors simultaneously without losing state

---

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/lnemenl/get_next_line.git
   cd get_next_line
   ```

2. Compile the library (with a buffer size of your choice):
   ```bash
   make
   gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 main.c get_next_line.a -o gnl
   ```

3. Clean up the compiled files (optional):
   ```bash
   make clean
   ```

---

## Usage
Include the header and call `get_next_line` in a loop:

```c
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>

int main(void)
{
    int fd = open("file.txt", O_RDONLY);
    char *line;

    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s", line);
        free(line);
    }
    close(fd);
    return (0);
}
```

Compile and run:

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 main.c get_next_line.a -o gnl
./gnl
```

### Example Output:
```
First line of the file  
Second line of the file  
Third line of the file
```

---

## How It Works
1. **File Reading:** Reads chunks of text into a buffer.  
2. **Line Extraction:** Extracts a line from the buffer (including the newline).  
3. **Persistent Buffering:** Uses a static variable to store leftover text between function calls.  
4. **Multiple FD Management (Bonus):** Keeps separate buffers for each file descriptor.

---

## Technical Insights
- **Static Variables:** Maintain state between function calls  
- **Dynamic Buffers:** Allocate and resize buffers to handle variable-length lines  
- **Memory Safety:** All allocated memory is properly freed, even on errors  

---

## Allowed Functions
- `read`, `malloc`, `free`

---

## License
This project is part of the 42 school curriculum. You are free to use it for learning purposes, but keep academic integrity in mind if you're a fellow student.

---

Built with care and attention to detail at 42.
