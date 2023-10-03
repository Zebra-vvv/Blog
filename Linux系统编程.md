# 文件I/O



## open函数

`open` 是一个操作系统提供的系统调用，用于打开文件或者创建新文件。它是在许多操作系统中（如Linux、Unix、Windows等）都存在的重要函数。`open` 函数提供了一种访问文件的方式，允许程序在文件上执行读取、写入以及其他操作。

在 Unix-like 操作系统中，`open` 函数的原型通常如下：

```c
int open(const char *pathname, int flags, mode_t mode);
```

其中各参数的含义如下：

- `pathname`：要打开或创建的文件路径名。

- `flags`：打开文件的标志，用于指定打开文件的模式和行为。这些标志可以通过位运算符 `|` 进行组合，例如 `O_RDONLY`、`O_WRONLY`、`O_RDWR`、`O_CREAT` 等。

- `mode`：当使用 `O_CREAT` 标志创建新文件时（不创建新文件时，无需使用这个参数），指定文件的权限。这通常是一个八进制的数值，例如 `0644` 表示文件权限。

    创建文件的最终权限 = mode &  ~umask

`open` 函数的返回值是一个文件描述符（file descriptor），它是一个整数，用于唯一标识打开的文件。通常，返回值为 0 或正整数表示成功打开文件，而返回值为 -1 表示打开文件失败，此时可以使用全局变量 `errno` 来获取具体的错误信息。

以下是一个示例用法：

```c
#include <fcntl.h>
#include <stdio.h>

int main() {
    int fd = open("example.txt", O_RDONLY);  // 打开 example.txt 文件为只读模式
    if (fd == -1) {
        perror("Failed to open file");
        return 1;
    }

    // 使用文件描述符进行读取、写入等操作

    close(fd);  // 关闭文件描述符
    return 0;
}
```

这个示例中使用了 `open` 函数打开一个名为 "example.txt" 的文件，并在失败时输出错误信息。之后的代码中可以使用获取到的文件描述符进行文件操作，最后通过 `close` 函数关闭文件描述符。



## close函数

`close` 是一个操作系统提供的系统调用，用于关闭文件描述符（file descriptor）。它用于终止程序对一个打开的文件或资源的访问，从而释放与该文件描述符相关的系统资源。

在 Unix-like 操作系统中，`close` 函数的原型通常如下：

```c
int close(int fd);
```

其中参数 `fd` 是要关闭的文件描述符。

`close` 函数的返回值是一个整数，通常为 0 表示成功，-1 表示关闭文件失败。如果关闭失败，可以通过查看全局变量 `errno` 来获取具体的错误信息。

以下是一个示例用法：

```c
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>

int main() {
    int fd = open("example.txt", O_RDONLY);
    if (fd == -1) {
        perror("Failed to open file");
        return 1;
    }

    // 使用文件描述符进行读取操作

    if (close(fd) == -1) {
        perror("Failed to close file");
        return 1;
    }

    return 0;
}
```

在这个示例中，首先使用 `open` 函数打开一个文件，然后进行一些读取操作，最后使用 `close` 函数关闭文件描述符。如果关闭失败，会输出错误信息。`close` 的目的是确保程序在不再需要文件描述符时释放相关的资源。



## read函数

`read` 是一个在操作系统中用于读取数据的系统调用，它允许程序从一个已打开的文件描述符（如文件、管道、套接字等）中读取数据。`read` 系统调用是操作系统提供的底层函数之一，用于处理输入操作。

在 Unix-like 操作系统中，`read` 系统调用的原型通常如下：

```c
ssize_t read(int fd, void *buf, size_t count);
```

其中各参数的含义如下：

- `fd`：要读取数据的文件描述符。
- `buf`：存放读取数据的缓冲区的指针。
- `count`：要读取的字节数。

`read` 系统调用的返回值是读取的字节数。如果返回值为 0，则表示已达到文件末尾；如果返回值为 -1，则表示出现了错误，这时可以通过查看全局变量 `errno` 来获取具体的错误信息。

需要注意的是，`read` 系统调用是一个较底层的操作，它操作的是文件描述符，而不是高级别的文件对象。因此，使用 `read` 需要注意缓冲区的管理和数据处理。

以下是一个示例用法：

```c
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>

int main() {
    int fd = open("example.txt", O_RDONLY);
    if (fd == -1) {
        perror("Failed to open file");
        return 1;
    }

    char buffer[100];  // 缓冲区用于存放读取的数据
    ssize_t bytesRead = read(fd, buffer, sizeof(buffer));
    if (bytesRead == -1) {
        perror("Failed to read from file");
        close(fd);
        return 1;
    }

    close(fd);

    printf("Read %zd bytes: %.*s\n", bytesRead, (int)bytesRead, buffer);

    return 0;
}
```

这个示例使用了 `read` 系统调用来从文件中读取数据，并将读取的数据输出到标准输出流。同样地，如果读取失败，会输出错误信息。



## write函数

`write` 是一个在操作系统中用于写入数据的系统调用，它允许程序将数据写入到一个已打开的文件描述符（如文件、管道、套接字等）。`write` 系统调用是操作系统提供的底层函数之一，用于处理输出操作。

在 Unix-like 操作系统中，`write` 系统调用的原型通常如下：

```c
ssize_t write(int fd, const void *buf, size_t count);
```

其中各参数的含义如下：

- `fd`：要写入数据的文件描述符。
- `buf`：存放待写入数据的缓冲区的指针。
- `count`：要写入的字节数。

`write` 系统调用的返回值是写入的字节数。如果返回值为 -1，则表示出现了错误，这时可以通过查看全局变量 `errno` 来获取具体的错误信息。

需要注意的是，`write` 系统调用是一个较底层的操作，它操作的是文件描述符，而不是高级别的文件对象。因此，使用 `write` 需要注意缓冲区的管理和数据处理。

以下是一个示例用法：

```c
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>

int main() {
    int fd = open("output.txt", O_WRONLY | O_CREAT, 0644);
    if (fd == -1) {
        perror("Failed to open file");
        return 1;
    }

    const char *message = "Hello, world!";
    ssize_t bytesWritten = write(fd, message, strlen(message));
    if (bytesWritten == -1) {
        perror("Failed to write to file");
        close(fd);
        return 1;
    }

    close(fd);

    printf("Wrote %zd bytes to file.\n", bytesWritten);

    return 0;
}
```

这个示例使用了 `write` 系统调用将数据写入到文件，并输出写入的字节数。同样地，如果写入失败，会输出错误信息。



### 练习：通过read和write系统调用来实现cp命令

```c
#include <unistd.h>
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[])
{
    char buf[1024];

    int n = 0;

    int fd1 = open(argv[1], O_RDONLY); // read
    if (fd1 == -1)
    {
        perror("open argv[1] error");
        exit(1);
    }

    int fd2 = open(argv[2], O_RDWR | O_CREAT | O_TRUNC, 0644);
    if (fd2 == -1)
    {
        perror("open argv[2] error");
        exit(1);
    }

    while ((n = read(fd1, buf, 1024)) != 0)
    {
        if (n == -1)
        {
            perror("read error");
            exit(1);
        }

        write(fd2, buf, n);
        if (n == -1)
        {
            perror("write error");
            exit(1);
        }
    }

    close(fd1);
    close(fd2);

    return 0;
}
```



### perror函数(库函数)

`perror` 是一个用于将错误信息输出到标准错误流的函数，它可以帮助开发者更方便地获取错误信息并进行错误处理。通常在遇到错误时，你可以使用 `perror` 函数输出详细的错误描述，以便更好地理解错误的原因。

在 C 语言中，`perror` 函数的原型如下：

```c
void perror(const char *s);
```

其中参数 `s` 是一个字符串，会被添加到错误信息之前，通常用来指明错误发生的上下文。

以下是一个示例用法：

```c
#include <stdio.h>
#include <errno.h>

int main() {
    FILE *file = fopen("nonexistent.txt", "r");
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    // 进一步的文件操作

    fclose(file);
    return 0;
}
```

在这个示例中，`fopen` 函数用于打开一个不存在的文件，然后使用 `perror` 函数输出错误信息。输出的信息会是形如 `"Error opening file: No such file or directory"`，其中 `"Error opening file"` 是由你提供的字符串，而 `"No such file or directory"` 是与错误码对应的错误描述。

通过在错误处理时使用 `perror` 函数，你可以更清楚地知道发生了什么错误，从而更好地进行调试和错误处理。



### exit函数(库函数)

`exit` 是一个 C 语言标准库中的函数，用于正常终止程序的执行。当程序调用 `exit` 函数时，它会立即终止当前程序的执行，并返回到调用程序（如操作系统或父进程）。`exit` 函数可以用于在程序中显式地退出，并且可以在退出时指定一个整数作为返回值，这个返回值通常用来传递程序的终止状态。

`exit` 函数的原型如下：

```c
void exit(int status);
```

其中 `status` 是一个整数值，表示程序的终止状态。通常情况下，返回 `0` 表示程序成功终止，而非零的返回值则表示程序异常终止，可以根据需要定义不同的状态码来表示不同的情况。

例如，一个简单的使用 `exit` 函数的示例：

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int result = some_operation();
    
    if (result != 0) {
        fprintf(stderr, "Error occurred: %d\n", result);
        exit(result);
    }
    
    printf("Program completed successfully.\n");
    return 0;
}
```

在这个示例中，如果 `some_operation` 函数返回非零的结果，程序将使用 `exit` 函数终止，并将结果作为状态码传递给调用程序。这可以帮助调用者了解程序的终止状态以及出现的错误情况。



## fcntl函数

`fcntl`（file control）是一个用于控制已打开文件描述符的功能的系统调用。它可以用于执行一系列对文件描述符进行操作的任务，如获取或设置文件状态标志、文件锁定、非阻塞 I/O 等。`fcntl` 函数在 Unix-like 操作系统中广泛使用。

`fcntl` 函数的原型如下：

```c
int fcntl(int fd, int cmd, ... /* arg */ );
```

- `fd`：表示文件描述符，即需要进行操作的文件描述符。

- `cmd`：是一个指定操作类型的参数。可以取以下值之一：
  - `F_DUPFD`：复制文件描述符。
  - `F_GETFL`：获取文件状态标志。
  - `F_SETFL`：设置文件状态标志。
  - `F_GETLK`：获取文件锁定信息。
  - `F_SETLK`：设置文件锁定。
  - `F_SETLKW`：设置文件锁定，阻塞等待。

- `arg`：是一个可选参数，取决于具体的 `cmd` 值。

以下是一些常见用法示例：

1. 获取和设置文件状态标志：
   ```c
   int flags = fcntl(fd, F_GETFL, 0); // 获取文件状态标志
   flags |= O_NONBLOCK; // 设置非阻塞标志
   fcntl(fd, F_SETFL, flags); // 设置文件状态标志
   ```

2. 复制文件描述符：
   ```c
   int new_fd = fcntl(old_fd, F_DUPFD, 0); // 复制文件描述符
   ```

3. 文件锁定：
   ```c
   struct flock lock;
   lock.l_type = F_WRLCK; // 写锁
   lock.l_whence = SEEK_SET;
   lock.l_start = 0;
   lock.l_len = 100;
   fcntl(fd, F_SETLKW, &lock); // 设置文件写锁定，并阻塞等待
   ```

`fcntl` 函数的使用可以帮助你管理文件描述符的属性和状态，实现文件锁定以及进行非阻塞 I/O 等操作。具体的用法会根据你的需求和平台而有所不同。



## lseek函数

当你使用 `lseek` 函数时，它允许你在已打开的文件中移动文件指针，从而实现文件的随机访问。

**函数的原型如下：**

```c
#include <unistd.h>
off_t lseek(int fd, off_t offset, int whence);
```

- `fd`：文件描述符，表示需要进行操作的文件。

- `offset`：移动的偏移量。根据 `whence` 参数的不同，偏移量可以相对于文件开头、当前位置或文件末尾进行计算。

- `whence`：标志，用于指定相对于哪个位置进行移动，可以取 `SEEK_SET`（文件开头）、`SEEK_CUR`（当前位置）或 `SEEK_END`（文件末尾）。

**应用场景：**

+ 文件的读写使用同一偏移位置
+ 获取文件的大小
+ 拓展文件大小(必须引起I/O操作才真正拓展)

**返回值：**

- 如果 `lseek` 调用成功，它将返回文件指针相对于文件开头的新位置。

- 如果 `lseek` 调用失败，它将返回 `-1`，同时你可以通过检查全局变量 `errno` 来获取具体的错误信息。

以下是一个示例，展示如何使用 `lseek` 函数进行文件的随机访问：

```c
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>
#include <errno.h>

int main() {
    int fd = open("file.txt", O_RDONLY);
    if (fd == -1) {
        perror("Error opening file");
        return 1;
    }

    // 将文件指针移动到偏移量为 50 处
    off_t new_offset = lseek(fd, 50, SEEK_SET);
    if (new_offset == -1) {
        perror("Error seeking in file");
        fprintf(stderr, "Error: %s\n", strerror(errno));
        close(fd);
        return 1;
    }

    // 从新位置读取数据
    char buffer[1024];
    ssize_t n = read(fd, buffer, sizeof(buffer));
    if (n > 0) {
        // 处理读取的数据
    }

    close(fd);
    return 0;
}
```

通过使用 `lseek`，你可以实现在文件中的任意位置进行读取或写入操作，从而有效地进行随机访问。同时，检查返回值和处理错误信息可以帮助你在使用 `lseek` 时更加安全和健壮。







## 文件描述符

 

### PCB进程控制块

**文件描述符（File Descriptor）**是一个在操作系统中用于标识和跟踪打开文件、管道、套接字等输入/输出资源的整数值。在 Unix-like 操作系统中，一切都被视为文件，包括硬盘上的文件、设备、管道、套接字等。文件描述符允许程序访问这些资源。

**本质：**一个结构体

**成员：**文件描述符表

**文件描述符表：**一个进程最多打开1024个文件(标号：0~1023)  。优先使用表中可用的最小标号。

以下是一些常见的文件描述符用途示例：

- `0`：标准输入（stdin）
- `1`：标准输出（stdout）
- `2`：标准错误输出（stderr）
- `3`、`4`、...：用户自定义的文件描述符，用于操作打开的文件、管道、套接字等。





## 阻塞和非阻塞



### 产生阻塞的场景

+ 读设备文件
+ 读网络文件
+ 常规文件无阻塞概念



**设备文件目录：**/dev/    (如：**终端**的目录：/dev/tty)



# 文件存储

`inode`（索引节点）和 `dentry`（目录项）是在 Unix-like 操作系统中用于管理文件系统的重要概念。



## **Inode（索引节点）**：

- `inode` 是文件系统中的一个数据结构，用于存储关于一个文件的元数据，如文件的权限、所有者、大小、时间戳等信息，以及文件数据的存储位置。
- 每个文件都对应一个唯一的 `inode`。这意味着即使在不同目录下有相同文件名的文件，它们的 `inode` 是不同的。
- `inode` 中存储的元数据允许操作系统和文件系统管理文件的属性和访问权限，并将文件的实际数据存储在存储块中。这种分离允许文件的不同硬链接共享同一个 `inode`，从而节省存储空间。
- 当文件被删除时，其关联的 `inode` 可能被标记为可回收，但实际的文件数据不会立即被删除。这是因为可能还有其他硬链接指向同一个 `inode`。



## **Dentry（目录项）**：

- `dentry` 是目录中的一个数据结构，用于存储目录中的文件和子目录的信息，包括文件名和对应的 `inode`。
- 目录中的每个文件或子目录都有一个关联的 `dentry` 条目。
- `dentry` 构成了目录树的基本元素，允许系统在文件系统中快速定位文件和目录。
- 当打开文件或访问目录时，操作系统会通过查找相应的 `dentry` 来找到对应的 `inode`，从而获取文件的元数据和数据。

综合起来，`inode` 和 `dentry` 是文件系统的关键组成部分，允许操作系统有效地管理文件和目录。`inode` 存储文件的元数据和数据块的位置，而 `dentry` 存储目录中的文件和子目录的信息，帮助系统实现文件系统的层次结构和查找。这两者的协同工作使得文件系统能够高效地存储、管理和访问文件。





# 文件操作



## stat函数

`stat` 是一个用于获取文件或文件夹的元数据信息（也称为文件状态）的系统调用。通过调用 `stat` 系统调用，你可以获取关于一个文件的各种信息，如文件类型、访问权限、所有者、大小、时间戳等。这些信息存储在一个名为 `struct stat` 的数据结构中。

`stat` 系统调用的原型如下：

```c
#include <sys/types.h>
#include <sys/stat.h>
int stat(const char *path, struct stat *buf);
```

- `path`：要获取元数据信息的文件或文件夹的路径。

- `buf`：指向一个 `struct stat` 结构的指针，用于存储获取到的文件状态信息。

`struct stat` 结构包含了许多字段，用于存储文件的不同属性。以下是一些常见的字段：

- `st_mode`：文件类型和访问权限。
- `st_size`：文件大小（字节）。
- `st_uid`：所有者的用户 ID。
- `st_gid`：所有者的组 ID。
- `st_atime`：最后访问时间。
- `st_mtime`：最后修改时间。
- `st_ctime`：最后状态更改时间（例如权限、所有者等变化时的时间）。

以下是一个使用 `stat` 系统调用的示例：

```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <unistd.h>

int main() {
    const char *file_path = "example.txt";
    struct stat file_info;

    if (stat(file_path, &file_info) == 0) {
        printf("File size: %ld bytes\n", file_info.st_size);
        printf("Owner's user ID: %d\n", file_info.st_uid);
        printf("Owner's group ID: %d\n", file_info.st_gid);
        // ... 其他信息
    } else {
        perror("Error getting file status");
        return 1;
    }

    return 0;
}
```

在这个示例中，我们使用 `stat` 系统调用获取了一个文件的元数据信息，并打印出一些信息，如文件大小、所有者的用户 ID 和组 ID。通过 `stat`，你可以了解有关文件的各种属性，以便更好地操作和处理文件。



## lstat函数

`lstat` 也是一个用于获取文件或文件夹的元数据信息的系统调用，类似于 `stat`。两者的主要区别在于对于符号链接的处理方式。

`lstat` 系统调用的原型如下：

```c
#include <sys/types.h>
#include <sys/stat.h>
int lstat(const char *path, struct stat *buf);
```

与 `stat` 类似，`lstat` 函数接受一个文件路径和一个指向 `struct stat` 结构的指针作为参数，用于存储获取到的文件状态信息。

区别在于：

- 当你使用 `stat` 获取符号链接文件的信息时，它会跟随符号链接指向的实际文件，并返回实际文件的信息。
- 而当你使用 `lstat` 获取符号链接文件的信息时，它只会获取符号链接本身的信息，而不会跟随符号链接。

这是因为符号链接是一个指向其他文件的引用，而 `lstat` 用于获取符号链接自身的信息，而不会递归地获取目标文件的信息。

以下是一个使用 `lstat` 系统调用的示例：

```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <unistd.h>

int main() {
    const char *link_path = "symlink_example";
    struct stat link_info;

    if (lstat(link_path, &link_info) == 0) {
        if (S_ISLNK(link_info.st_mode)) {
            printf("This is a symbolic link.\n");
        } else {
            printf("This is not a symbolic link.\n");
        }
        // ... 其他信息
    } else {
        perror("Error getting link status");
        return 1;
    }

    return 0;
}
```

在这个示例中，我们使用 `lstat` 系统调用获取了一个符号链接的信息，并根据文件类型进行判断。通过 `lstat`，你可以了解符号链接文件本身的信息，而不必跟随链接到的实际文件。



## link和unlink函数

`link` 和 `unlink` 是用于创建硬链接和删除文件的系统调用。

**`link` 系统调用**：
```c
#include <unistd.h>
int link(const char *oldpath, const char *newpath);
```

`link` 调用用于创建一个新的硬链接，将现有文件链接到新的文件名上。硬链接是指多个文件名指向同一个 `inode`，因此它们实际上是同一个文件的不同名字。新的硬链接会与现有的文件共享相同的数据和属性。要创建硬链接，`oldpath` 参数是现有文件的路径，`newpath` 参数是新的链接文件的路径。

**`unlink` 系统调用**：
```c
#include <unistd.h>
int unlink(const char *pathname);
```

`unlink` 调用用于删除一个文件的链接（也就是删除一个硬链接），当一个文件的所有硬链接都被删除时，文件的数据和元数据（如 `inode`）会被释放，从而删除文件。注意，`unlink` 仅会删除链接，而不会删除文件的实际数据，除非没有任何链接指向该文件。在某些情况下，它也可以用于删除符号链接。

以下是一个简单的示例，展示如何使用 `link` 和 `unlink` 系统调用：

```c
#include <unistd.h>
#include <stdio.h>

int main() {
    // 创建硬链接
    if (link("source.txt", "hardlink.txt") == 0) {
        printf("Hard link created.\n");
    } else {
        perror("Error creating hard link");
        return 1;
    }

    // 删除硬链接
    if (unlink("hardlink.txt") == 0) {
        printf("Hard link deleted.\n");
    } else {
        perror("Error deleting hard link");
        return 1;
    }

    return 0;
}
```

在这个示例中，我们首先使用 `link` 创建了一个硬链接，然后使用 `unlink` 删除了这个硬链接。通过这些系统调用，你可以在文件系统中创建硬链接并删除链接。



## readlink函数

`readlink` 是一个用于读取符号链接内容的系统调用。

**`readlink` 系统调用**：
```c
#include <unistd.h>
ssize_t readlink(const char *pathname, char *buf, size_t bufsiz);
```

`readlink` 调用用于读取符号链接的内容。它接受一个符号链接的路径作为 `pathname` 参数，将符号链接的内容存储在指定的缓冲区 `buf` 中。`bufsiz` 参数指定了缓冲区的大小，确保缓冲区足够大以容纳符号链接的内容。`readlink` 调用返回实际读取的字节数，如果出错则返回 `-1`。

以下是一个简单的示例，展示如何使用 `readlink` 系统调用来读取符号链接的内容：

```c
#include <unistd.h>
#include <stdio.h>
#include <string.h>

int main() {
    char buf[1024]; // 用于存储符号链接内容的缓冲区

    ssize_t size = readlink("symlink_example", buf, sizeof(buf) - 1);
    if (size != -1) {
        buf[size] = '\0'; // 在读取的内容后添加字符串终止符
        printf("Symbolic link content: %s\n", buf);
    } else {
        perror("Error reading symbolic link");
        return 1;
    }

    return 0;
}
```

在这个示例中，我们使用 `readlink` 读取了一个符号链接的内容，并将内容存储在缓冲区 `buf` 中。注意，我们在读取内容后添加了字符串终止符，以确保内容在打印时以字符串形式正确显示。

通过使用 `readlink`，你可以获取符号链接所指向的实际路径或目标。



## rename函数

`rename` 是一个用于重命名文件或将文件移动到不同位置的系统调用。

**`rename` 系统调用**：

```c
#include <stdio.h>
int rename(const char *oldpath, const char *newpath);
```

`rename` 调用用于将现有文件或目录从一个名称重命名为另一个名称，或者将文件移动到不同的路径。`oldpath` 参数是现有文件或目录的路径，`newpath` 参数是新的文件或目录的路径。

以下是一个示例，展示如何使用 `rename` 系统调用来重命名文件：

```c
#include <stdio.h>

int main() {
    const char *oldname = "oldfile.txt";
    const char *newname = "newfile.txt";

    if (rename(oldname, newname) == 0) {
        printf("File renamed successfully.\n");
    } else {
        perror("Error renaming file");
        return 1;
    }

    return 0;
}
```

在这个示例中，我们使用 `rename` 将文件从 "oldfile.txt" 重命名为 "newfile.txt"。这个调用也可以用于将文件移动到不同的路径，只要 `newpath` 参数指定了不同的路径。

需要注意的是，`rename` 调用不能用于对目录进行递归地移动或重命名，如果你需要对目录进行操作，可能需要使用更复杂的方法来完成。



# 文件目录



## getcwd函数

`getcwd` 是一个用于获取当前工作目录路径的系统调用。

**`getcwd` 系统调用**：
```c
#include <unistd.h>
char *getcwd(char *buf, size_t size);
```

`getcwd` 调用用于获取当前工作目录的路径。它接受一个字符数组 `buf` 作为缓冲区，用于存储当前工作目录的路径。参数 `size` 指定了缓冲区的大小。

如果 `buf` 缓冲区足够大以容纳当前工作目录的路径，`getcwd` 调用将路径存储在 `buf` 中，并返回指向 `buf` 的指针。如果缓冲区大小不足以容纳路径，或者调用出现错误，`getcwd` 将返回 `NULL`。

以下是一个示例，展示如何使用 `getcwd` 系统调用来获取当前工作目录的路径：

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    char buf[1024]; // 用于存储当前工作目录路径的缓冲区

    if (getcwd(buf, sizeof(buf)) != NULL) {
        printf("Current working directory: %s\n", buf);
    } else {
        perror("Error getting working directory");
        return 1;
    }

    return 0;
}
```

在这个示例中，我们使用 `getcwd` 获取当前工作目录的路径，并将路径存储在缓冲区 `buf` 中。通过这个调用，你可以了解程序当前的工作目录，以便在文件操作中使用正确的路径。



## chdir函数

`chdir` 是一个用于改变当前工作目录的系统调用。

**`chdir` 系统调用**：
```c
#include <unistd.h>
int chdir(const char *path);
```

`chdir` 调用用于将当前进程的工作目录更改为指定的路径。`path` 参数是新的工作目录路径。

以下是一个示例，展示如何使用 `chdir` 系统调用来改变当前工作目录：

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    const char *new_directory = "/path/to/new_directory";

    if (chdir(new_directory) == 0) {
        printf("Current working directory changed to: %s\n", new_directory);
    } else {
        perror("Error changing working directory");
        return 1;
    }

    return 0;
}
```

在这个示例中，我们使用 `chdir` 将当前工作目录更改为指定的路径。通过这个调用，你可以在程序中动态地改变当前的工作目录，以便在文件操作等情况下使用正确的路径。需要注意的是，工作目录的改变在当前进程中生效，不会影响其他进程。



## opendir函数

`opendir` 是一个用于打开目录的函数，通常用于读取目录中的文件和子目录。

**`opendir` 函数**：

```c
#include <dirent.h>
DIR *opendir(const char *dirname);
```

- `opendir` 函数接受一个参数 `dirname`，该参数是要打开的目录的路径。它返回一个指向 `DIR` 结构的指针，该结构表示打开的目录流（或者说目录句柄）。

一旦成功打开目录，你就可以使用其他 `readdir` 系统调用或函数来读取目录中的文件和子目录的信息。这些信息通常包括文件名、文件类型等。

以下是一个示例，展示如何使用 `opendir` 和 `readdir` 函数来列出目录中的文件和子目录：

```c
#include <stdio.h>
#include <dirent.h>

int main() {
    const char *directory_path = "/path/to/directory";
    DIR *dir;
    struct dirent *entry;

    dir = opendir(directory_path);

    if (dir != NULL) {
        printf("Listing files and subdirectories in %s:\n", directory_path);

        while ((entry = readdir(dir)) != NULL) {
            printf("%s\n", entry->d_name);
        }

        closedir(dir);
    } else {
        perror("Error opening directory");
        return 1;
    }

    return 0;
}
```

在这个示例中，我们首先使用 `opendir` 打开一个目录，然后使用 `readdir` 循环读取目录中的文件和子目录的信息，并打印它们的名字。最后，我们使用 `closedir` 关闭目录句柄。通过这种方式，你可以遍历目录中的内容。



## closedir函数

`closedir` 是一个用于关闭已打开目录的函数。

**`closedir` 函数**：

```c
#include <dirent.h>
int closedir(DIR *dir);
```

- `closedir` 函数接受一个参数 `dir`，该参数是一个指向已打开目录的指针，表示要关闭的目录流（或者说目录句柄）。

一旦你使用 `opendir` 打开了一个目录，并完成了对该目录的操作，最好使用 `closedir` 函数来关闭目录，以释放系统资源并确保不会继续访问已关闭的目录。

以下是一个示例，展示如何使用 `closedir` 函数来关闭一个已打开的目录：

```c
#include <stdio.h>
#include <dirent.h>

int main() {
    const char *directory_path = "/path/to/directory";
    DIR *dir;
    struct dirent *entry;

    dir = opendir(directory_path);

    if (dir != NULL) {
        printf("Listing files and subdirectories in %s:\n", directory_path);

        while ((entry = readdir(dir)) != NULL) {
            printf("%s\n", entry->d_name);
        }

        closedir(dir); // 关闭目录

    } else {
        perror("Error opening directory");
        return 1;
    }

    return 0;
}
```

在这个示例中，我们在完成对目录的操作后使用 `closedir` 函数关闭了已打开的目录。这是一个良好的编程实践，以确保及时释放资源并避免不必要的问题。



## readdir函数

`readdir` 是一个用于读取目录中的文件和子目录信息的函数。

**`readdir` 函数**：
```c
#include <dirent.h>
struct dirent *readdir(DIR *dir);
```

- `readdir` 函数接受一个参数 `dir`，该参数是一个指向已打开目录的指针，表示要读取的目录流（或者说目录句柄）。

- `readdir` 函数返回一个指向 `struct dirent` 结构的指针，该结构包含了读取的目录项的信息，包括文件名、文件类型等。如果目录中没有更多的条目可读，或者发生了错误，`readdir` 返回 `NULL`。

通过多次调用 `readdir` 函数，你可以逐个读取目录中的文件和子目录的信息，直到达到目录的末尾或出现错误为止。

以下是一个示例，展示如何使用 `readdir` 函数来列出目录中的文件和子目录：

```c
#include <stdio.h>
#include <dirent.h>

int main() {
    const char *directory_path = "/path/to/directory";
    DIR *dir;
    struct dirent *entry;

    dir = opendir(directory_path);

    if (dir != NULL) {
        printf("Listing files and subdirectories in %s:\n", directory_path);

        while ((entry = readdir(dir)) != NULL) {
            printf("%s\n", entry->d_name);
        }

        closedir(dir);

    } else {
        perror("Error opening directory");
        return 1;
    }

    return 0;
}
```

在这个示例中，我们使用 `readdir` 在循环中读取目录中的文件和子目录信息，并打印它们的名字。一旦 `readdir` 返回 `NULL`，表示已经读取完目录中的所有内容。



# 重定向



## dup和dup2函数

`dup` 和 `dup2` 是用于复制文件描述符的系统调用，它们可以用于创建新的文件描述符，指向与原始文件描述符相同的文件或资源。这对于在程序中重定向输入、输出或错误流非常有用。

**`dup` 系统调用**：
```c
#include <unistd.h>
int dup(int oldfd);
```

- `dup` 函数接受一个参数 `oldfd`，该参数是要复制的文件描述符。
- `dup` 调用会创建一个新的文件描述符，该描述符与 `oldfd` 所指向的文件或资源相同。
- 新的文件描述符通常是当前可用的文件描述符中的最小值。

以下是一个示例，展示如何使用 `dup` 系统调用来复制文件描述符：

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    int fd1, fd2;

    // 打开一个文件
    fd1 = open("file.txt", O_RDONLY);

    if (fd1 != -1) {
        // 复制文件描述符
        fd2 = dup(fd1);

        if (fd2 != -1) {
            printf("File descriptors: %d (fd1), %d (fd2)\n", fd1, fd2);
            // 可以使用 fd1 和 fd2 进行文件读取等操作
            close(fd1);
            close(fd2);
        } else {
            perror("Error duplicating file descriptor");
            close(fd1);
            return 1;
        }
    } else {
        perror("Error opening file");
        return 1;
    }

    return 0;
}
```

在这个示例中，我们首先使用 `open` 函数打开一个文件，然后使用 `dup` 复制文件描述符 `fd1`，创建了一个新的文件描述符 `fd2`，它们都指向同一个文件。接着，我们可以使用这两个文件描述符进行文件操作。

**`dup2` 系统调用**：
```c
#include <unistd.h>
int dup2(int oldfd, int newfd);
```

- `dup2` 函数接受两个参数 `oldfd` 和 `newfd`，其中 `oldfd` 是要复制的文件描述符，`newfd` 是指定的新文件描述符。
- `dup2` 调用会将 `newfd` 指向 `oldfd` 所指向的文件或资源，如果 `newfd` 已经打开，它将先关闭 `newfd`，然后再指向 `oldfd`。
- 这允许你将一个文件描述符复制到指定的文件描述符，而不仅仅是最小可用的文件描述符。

以下是一个示例，展示如何使用 `dup2` 系统调用来复制文件描述符到指定的文件描述符：

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    int fd1, fd2;

    // 打开一个文件
    fd1 = open("file.txt", O_RDONLY);

    if (fd1 != -1) {
        // 复制文件描述符到指定的文件描述符
        fd2 = 10; // 假设新的文件描述符是 10
        if (dup2(fd1, fd2) != -1) {
            printf("File descriptors: %d (fd1), %d (fd2)\n", fd1, fd2);
            // 可以使用 fd1 和 fd2 进行文件读取等操作
            close(fd1);
        } else {
            perror("Error duplicating file descriptor");
            close(fd1);
            return 1;
        }
    } else {
        perror("Error opening file");
        return 1;
    }

    return 0;
}
```

在这个示例中，我们使用 `dup2` 复制文件描述符 `fd1` 到指定的文件描述符 `fd2`（这里假设 `fd2` 是 10）。如果 `fd2` 已经打开，`dup2` 会关闭 `fd2`，然后将其指向 `fd1`。这样，我们可以将文件描述符复制到指定的文件描述符，而不仅仅是最小可用的文件描述符。



# 进程控制



## fork函数

`fork` 函数是一个用于创建新进程的系统调用。在调用 `fork` 函数后，将创建一个新的进程，该进程是调用进程的一个副本，被称为子进程。子进程将执行与父进程相同的程序代码，但是有不同的进程 ID（PID）。

**`fork` 系统调用**：
```c
#include <unistd.h>
pid_t fork(void);
```

- `fork` 调用没有参数，它会创建一个新的进程，该进程是调用进程的副本。
- 在父进程中，`fork` 调用返回子进程的 PID（正整数），这个 PID 可以用来识别和管理子进程。
- 在子进程中，`fork` 调用返回 0，以表示子进程。

以下是一个示例，展示如何使用 `fork` 创建一个子进程：

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    pid_t pid; // 用于存储进程 ID

    // 调用 fork 创建子进程
    pid = fork();

    if (pid == -1) {
        perror("Error creating child process");
        return 1;
    }

    if (pid == 0) {
        // 子进程的代码
        printf("Child process (PID %d) is running.\n", getpid());
    } else {
        // 父进程的代码
        printf("Parent process (PID %d) created child process (PID %d).\n", getpid(), pid);
    }

    return 0;
}
```

在这个示例中，我们调用 `fork` 创建了一个子进程。在父进程中，`fork` 返回子进程的 PID，而在子进程中，`fork` 返回 0。通过检查返回值，我们可以在代码中区分父进程和子进程，并执行不同的操作。

需要注意的是，子进程是父进程的副本，包括程序代码、变量等，但它们在不同的进程空间中运行，彼此不会相互干扰。这使得多进程编程成为可能，每个进程可以执行不同的任务。



## getpid和getppid函数

`getpid` 和 `getppid` 是用于获取进程 ID（PID）和父进程 ID（PPID）的系统调用。

**`getpid` 系统调用**：
```c
#include <unistd.h>
pid_t getpid(void);
```

- `getpid` 调用没有参数，用于获取当前进程的 PID。
- 返回值是一个 `pid_t` 类型的整数，表示当前进程的 PID。

**`getppid` 系统调用**：
```c
#include <unistd.h>
pid_t getppid(void);
```

- `getppid` 调用没有参数，用于获取当前进程的父进程的 PID。
- 返回值是一个 `pid_t` 类型的整数，表示当前进程的父进程的 PID。

以下是一个示例，展示如何使用 `getpid` 和 `getppid` 系统调用来获取进程的 PID 和父进程的 PID：

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    pid_t pid, parent_pid;

    pid = getpid(); // 获取当前进程的 PID
    parent_pid = getppid(); // 获取当前进程的父进程的 PID

    printf("Current process PID: %d\n", pid);
    printf("Parent process PID: %d\n", parent_pid);

    return 0;
}
```

在这个示例中，我们分别使用 `getpid` 和 `getppid` 获取当前进程的 PID 和父进程的 PID，并将它们打印出来。这些系统调用通常用于识别和管理进程。



## exec函数族

`exec` 函数族是一组用于执行新程序的系统调用，它们允许在一个进程中启动另一个程序，替换当前进程的映像并加载新程序。这些函数通常用于实现程序的替换和执行外部命令的功能。以下是 `exec` 函数族的一些主要成员：

1. **`execve`**：这是最通用的 `exec` 函数，允许你指定程序路径、命令行参数和环境变量。它的原型如下：

   ```c
   #include <unistd.h>
   int execve(const char *pathname, char *const argv[], char *const envp[]);
   ```

   - `pathname` 是要执行的程序的路径。
   - `argv` 是一个字符串数组，包含命令行参数，以 `NULL` 结尾。
   - `envp` 是一个字符串数组，包含环境变量，以 `NULL` 结尾。

2. **`execv` 和 `execvp`**：这两个函数允许你指定程序路径和命令行参数，但不需要传递环境变量。它们的原型如下：

   ```c
   #include <unistd.h>
   int execv(const char *pathname, char *const argv[]);
   int execvp(const char *file, char *const argv[]);
   ```

   - `pathname` 或 `file` 是要执行的程序的路径或文件名。
   - `argv` 是一个字符串数组，包含命令行参数，以 `NULL` 结尾。
   - `execvp` 允许在 `PATH` 环境变量指定的目录中查找可执行文件。

3. **`execl` 和 `execlp`**：这两个函数允许你以可变参数的形式指定程序路径和命令行参数，但不需要传递环境变量。它们的原型如下：

   ```c
   #include <unistd.h>
   int execl(const char *pathname, const char *arg, ... /* (char *) NULL */ );
   int execlp(const char *file, const char *arg, ... /* (char *) NULL */ );
   ```

   - `pathname`、`file` 和 `arg` 是字符串参数，用于指定程序路径和命令行参数，以 `NULL` 结尾。
   - `execlp` 允许在 `PATH` 环境变量指定的目录中查找可执行文件。

4. **`execle`**：这个函数允许你指定程序路径、命令行参数和环境变量，以可变参数的形式传递。它的原型如下：

   ```c
   #include <unistd.h>
   int execle(const char *pathname, const char *arg, ... /* (char *) NULL, char *const envp[] */ );
   ```

   - `pathname` 是要执行的程序的路径。
   - `arg` 是字符串参数，用于指定命令行参数，以 `NULL` 结尾。
   - `envp` 是一个字符串数组，包含环境变量，以 `NULL` 结尾。

这些 `exec` 函数族的成员允许你以不同的方式执行新程序，替换当前进程的映像。选择使用哪个函数取决于你的需求，包括是否需要传递环境变量、如何传递参数等。通过这些函数，你可以在一个进程内启动其他程序，实现了程序的替换和执行外部命令的功能。



## wait函数

`wait` 函数是一个用于等待子进程结束并获取其退出状态的系统调用。它允许父进程等待其子进程执行完毕，以便获取子进程的终止状态信息。`wait` 函数通常与 `fork` 一起使用，以确保父进程在子进程完成后进行处理。

**`wait` 系统调用**：
```c
#include <sys/types.h>
#include <sys/wait.h>
pid_t wait(int *status);
```

- `wait` 调用没有参数，但接受一个 `status` 指针，用于存储子进程的终止状态信息。
- 如果 `wait` 成功等待到一个子进程终止，它将返回被终止的子进程的PID。
- 如果 `status` 不为 NULL，那么子进程的退出状态信息将被存储在 `status` 中。这个信息包括子进程的退出码以及退出的原因。

以下是一个示例，展示如何使用 `fork` 和 `wait` 函数来创建一个子进程，并在父进程中等待子进程执行完毕：

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    pid_t pid;
    int status;

    // 创建子进程
    pid = fork();

    if (pid == -1) {
        perror("Error creating child process");
        return 1;
    }

    if (pid == 0) {
        // 子进程的代码
        printf("Child process (PID %d) is running.\n", getpid());
        exit(42); // 子进程退出并返回退出码 42
    } else {
        // 父进程的代码
        printf("Parent process (PID %d) created child process (PID %d).\n", getpid(), pid);

        // 等待子进程结束并获取其退出状态
        wait(&status);

        if (WIFEXITED(status)) {
            printf("Child process exited with status: %d\n", WEXITSTATUS(status));
        }
    }

    return 0;
}
```

在这个示例中，父进程通过 `fork` 创建了一个子进程，并使用 `wait` 函数等待子进程结束。一旦子进程结束，父进程可以通过 `WIFEXITED` 和 `WEXITSTATUS` 宏获取子进程的退出状态信息，包括退出码。这允许父进程了解子进程的执行结果。



## waitpid函数

`waitpid` 函数是一个用于等待指定子进程结束并获取其退出状态的系统调用。与 `wait` 函数不同，`waitpid` 允许你精确指定要等待的子进程，以及是否要非阻塞地等待子进程的终止。这使得它更加灵活，通常用于多进程管理场景。

**`waitpid` 系统调用**：
```c
#include <sys/types.h>
#include <sys/wait.h>
pid_t waitpid(pid_t pid, int *status, int options);
```

- `pid` 参数用于指定要等待的子进程的PID。具体取值如下：
  - 如果 `pid` 为负数，表示等待任意子进程，相当于 `wait`。
  - 如果 `pid` 为0，表示等待与调用进程组ID相同的任意子进程。
  - 如果 `pid` 大于0，表示等待具有指定PID的子进程。
- `status` 参数是一个指向整数的指针，用于存储子进程的终止状态信息，包括退出码和退出原因。
- `options` 参数用于指定等待的选项，可以使用按位或运算符 `|` 组合多个选项，常用选项有：
  - `WNOHANG`：非阻塞等待，如果没有子进程退出，立即返回0。
  - `WUNTRACED`：同时等待已经停止的子进程，通常用于处理作业控制。
  - `WCONTINUED`：等待已经继续的子进程，通常用于处理作业控制。

以下是一个示例，展示如何使用 `waitpid` 函数来等待指定子进程的终止：

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    pid_t pid;
    int status;

    // 创建子进程
    pid = fork();

    if (pid == -1) {
        perror("Error creating child process");
        return 1;
    }

    if (pid == 0) {
        // 子进程的代码
        printf("Child process (PID %d) is running.\n", getpid());
        sleep(2); // 子进程休眠 2 秒
        exit(42); // 子进程退出并返回退出码 42
    } else {
        // 父进程的代码
        printf("Parent process (PID %d) created child process (PID %d).\n", getpid(), pid);

        // 等待指定子进程结束并获取其退出状态
        pid_t terminated_pid = waitpid(pid, &status, 0);

        if (terminated_pid == -1) {
            perror("Error waiting for child process");
        } else if (WIFEXITED(status)) {
            printf("Child process (PID %d) exited with status: %d\n", terminated_pid, WEXITSTATUS(status));
        }
    }

    return 0;
}
```

在这个示例中，父进程使用 `waitpid` 函数等待指定的子进程（由 `pid` 参数指定）结束，并获取其退出状态信息。如果子进程在等待期间退出，父进程将获得子进程的退出状态信息，包括退出码。如果子进程尚未退出，父进程可以选择阻塞等待或立即返回，这由 `options` 参数控制。



# 进程通信(IPC)



## 管道

管道（Pipe）是一种在操作系统中用于进程间通信的机制。它允许一个进程将数据发送到另一个进程，从而实现这两个进程之间的数据交换。管道通常用于在父子进程或者不相关的进程之间传递数据。

**特质：**

1. 伪文件
2. 管道中的数据只能一次读取
3. 数据在管道中，只能单向流动

**局限性：**

1. 自己写，不能自己读
2. 数据不可以反复读
3. 半双工通信
4. 只有血缘关系进程间可用

在C语言中，可以使用 `pipe` 系统调用来创建管道，使用 `read` 和 `write` 系统调用来读写管道数据。例如，一个进程可以将数据写入一个管道，而另一个进程可以从同一管道读取数据，从而实现进程间的数据传输。

总之，管道是一种用于在进程之间传递数据的有用工具，它允许进程进行简单而高效的通信，通常用于构建数据处理流水线和实现进程间协作。



## pipe函数

`pipe` 函数是一个系统调用，用于创建匿名管道（Anonymous Pipe），它是一种用于进程间通信的机制，允许一个进程将数据写入管道，另一个进程从管道中读取数据。`pipe` 函数通常用于在父子进程之间或者不相关的进程之间传递数据。

**`pipe` 系统调用**：
```c
#include <unistd.h>
int pipe(int pipefd[2]);
```

- `pipefd` 是一个长度为 2 的整数数组，用于存储管道的文件描述符。`pipefd[0]` 表示读取管道的文件描述符，`pipefd[1]` 表示写入管道的文件描述符。
- `pipe` 调用成功时返回 0，失败时返回 -1。

以下是一个示例，展示如何使用 `pipe` 函数创建一个管道并在父子进程之间传递数据：

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    int pipefd[2];
    pid_t pid;
    char buffer[1024];

    // 创建管道
    if (pipe(pipefd) == -1) {
        perror("Error creating pipe");
        return 1;
    }

    // 创建子进程
    pid = fork();

    if (pid == -1) {
        perror("Error creating child process");
        return 1;
    }

    if (pid == 0) {
        // 子进程的代码
        close(pipefd[1]); // 关闭写入管道的文件描述符

        // 从管道中读取数据
        read(pipefd[0], buffer, sizeof(buffer));
        printf("Child process received data: %s\n", buffer);

        close(pipefd[0]); // 关闭读取管道的文件描述符
        exit(0);
    } else {
        // 父进程的代码
        close(pipefd[0]); // 关闭读取管道的文件描述符

        // 向管道中写入数据
        const char *message = "Hello, child process!";
        write(pipefd[1], message, strlen(message) + 1);

        close(pipefd[1]); // 关闭写入管道的文件描述符

        wait(NULL); // 等待子进程结束

        printf("Parent process finished.\n");
    }

    return 0;
}
```

在这个示例中，父进程使用 `pipe` 函数创建了一个管道，然后创建了一个子进程。父进程向管道中写入数据，而子进程从管道中读取数据，并在标准输出上显示接收到的消息。管道允许父子进程之间进行通信，实现了进程间数据传递的功能。需要注意的是，父子进程需要在使用完管道后关闭相应的文件描述符，以确保管道正常工作。



## FIFO

FIFO（First-In-First-Out），也称为命名管道（Named Pipe），是一种在Unix和类Unix操作系统中用于进程间通信的特殊文件类型。它允许不相关的进程通过文件系统路径来进行通信，类似于使用普通文件。FIFO是有名的，因为它们具有文件系统路径和名称，可以在文件系统中创建和访问。

以下是FIFO的主要特点和概念：

1. **命名管道**：与匿名管道不同，FIFO是命名的，它们具有在文件系统中的路径和名称，允许多个进程通过打开和读写相同的FIFO文件来进行通信。

2. **进程间通信**：FIFO是用于不相关的进程之间进行通信的一种方式。一个进程可以将数据写入FIFO，而另一个进程可以从FIFO中读取相同的数据。

3. **半双工**：FIFO通常是半双工的，这意味着它们可以在一个方向上传输数据。如果需要双向通信，通常需要创建两个FIFO，一个用于每个方向。

4. **阻塞**：当进程尝试从一个空的FIFO中读取数据或者向一个满的FIFO中写入数据时，它们可能会被阻塞，直到另一个进程进行相应的操作。这使得FIFO适用于同步进程间的通信。

5. **文件系统路径**：FIFO以文件系统路径的形式存在，类似于普通文件。它们可以通过路径名来引用。

6. **权限控制**：FIFO遵循文件系统的权限控制规则，可以限制哪些进程可以访问它们。

在C语言中，可以使用`mkfifo`函数创建FIFO，然后使用标准文件I/O函数（例如`open`、`read`和`write`）来读写FIFO中的数据。以下是一个简单的示例，展示如何创建和使用FIFO进行进程间通信：

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>

int main() {
    const char *fifoPath = "/tmp/my_fifo"; // FIFO的路径
    char buffer[1024];
    
    // 创建FIFO
    if (mkfifo(fifoPath, 0666) == -1) {
        perror("Error creating FIFO");
        return 1;
    }

    // 打开FIFO以供写入
    int fd = open(fifoPath, O_WRONLY);
    if (fd == -1) {
        perror("Error opening FIFO for writing");
        return 1;
    }

    // 向FIFO中写入数据
    const char *message = "Hello, FIFO!";
    write(fd, message, strlen(message) + 1);
    close(fd);

    // 打开FIFO以供读取
    fd = open(fifoPath, O_RDONLY);
    if (fd == -1) {
        perror("Error opening FIFO for reading");
        return 1;
    }

    // 从FIFO中读取数据
    read(fd, buffer, sizeof(buffer));
    printf("Received data from FIFO: %s\n", buffer);
    close(fd);

    return 0;
}
```

在此示例中，一个进程创建了一个FIFO并打开它以供写入，然后另一个进程打开相同的FIFO以供读取。这两个进程可以通过FIFO进行通信，实现了进程间的数据传递。需要注意的是，FIFO的创建和打开需要适当的错误处理和权限设置。



# 存储映射I/O



## mmap函数

`mmap`（Memory Map）函数是一个用于在进程的地址空间中创建内存映射区域的系统调用。它允许进程将一个文件或匿名内存映射到其地址空间中，以便直接访问文件内容或共享内存，而无需使用标准的文件I/O函数。

`mmap` 函数的原型如下：

```c
#include <sys/mman.h>
void *mmap(void *addr, size_t length, int prot, int flags, int fd, off_t offset);
```

参数解释如下：

- `addr`：指定映射区域的起始地址，通常设置为 `NULL`，以便由系统自动选择一个合适的地址。
- `length`：映射区域的长度，以字节为单位。
- `prot`：指定内存保护权限，可以使用以下标志的按位或组合：
  - `PROT_READ`：允许读取映射区域。
  - `PROT_WRITE`：允许写入映射区域。
  - `PROT_EXEC`：允许执行映射区域。
  - `PROT_NONE`：禁止所有访问权限。
- `flags`：用于控制映射区域的特性，可以使用以下标志的按位或组合：
  - `MAP_SHARED`：允许多个进程共享映射区域，对映射区域的更改会反映到底层文件。
  - `MAP_PRIVATE`：创建一个私有映射区域，对映射区域的更改不会反映到底层文件。
  - `MAP_ANONYMOUS`：创建匿名映射区域，不与文件关联，通常与 `MAP_PRIVATE` 一起使用。
  - `MAP_FIXED`：要求映射区域必须从指定的地址开始，如果无法满足，则映射失败。
- `fd`：如果要映射文件，这是打开文件的文件描述符；如果不映射文件，通常设置为 `-1`。
- `offset`：映射文件时，指定文件中的偏移量；不映射文件时，通常设置为 `0`。

`mmap` 函数成功时返回映射区域的起始地址，失败时返回 `MAP_FAILED`（通常是 `(void *) -1`）。一旦映射成功，进程可以通过指针直接访问映射区域中的数据，而不需要使用标准文件I/O函数。映射区域的更改可以反映到底层文件（如果使用 `MAP_SHARED` 标志），也可以只影响进程的私有副本（如果使用 `MAP_PRIVATE` 标志）。

`mmap` 函数常用于以下情况：

- 创建共享内存区域，允许多个进程共享数据。
- 在内存中映射大文件，以减少文件I/O操作的次数。
- 实现内存映射文件，以便将文件内容作为内存数组进行访问。
- 实现零拷贝数据传输，例如，将数据从网络套接字直接映射到内存中。

需要注意的是，使用 `mmap` 函数需要谨慎处理内存映射区域的权限和生命周期，以避免内存泄漏和潜在的安全问题。





































