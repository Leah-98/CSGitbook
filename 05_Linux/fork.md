`fork()` 是一个 Unix 系统调用，用于创建一个新的进程。它的原理涉及到操作系统的内存管理和进程控制机制：

1. **复制父进程**：当调用 `fork()` 时，操作系统会创建一个新的进程，称为子进程。子进程的内存空间会完全复制父进程的内存空间，包括代码段、数据段、堆和栈。这意味着子进程会得到一个父进程的副本，但是它们各自有独立的内存空间，互不干扰。
2. **共享文件描述符**：父进程和子进程之间共享打开的文件描述符。这意味着如果一个进程在 `fork()` 之前打开了文件，那么在 `fork()` 之后，子进程也会继承这些文件描述符，并且它们会指向相同的文件表项。但是，父子进程之间的文件描述符是独立的，关闭一个进程的文件描述符不会影响另一个进程。
3. **返回值**：在父进程中，`fork()` 返回子进程的进程 ID（PID），而在子进程中，`fork()` 返回 0。这样可以通过返回值来区分父进程和子进程。
4. **进程状态**：子进程是一个全新的进程，与父进程并行运行。子进程的状态会被设置为就绪状态，然后由调度器决定何时运行。

总的来说，`fork()` 的原理是通过复制父进程的内存空间来创建一个新的进程，使得父子进程可以并行运行，并且共享一些资源，例如文件描述符。这种机制为 Unix 系统提供了一种高效的多任务处理方式。