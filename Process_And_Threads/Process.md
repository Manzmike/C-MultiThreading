# Understanding Processes vs Threads
## **Example: Process Creation Using fork()**
## This example demonstrates how to create a new process using the fork() system call in C.



## Code:
```c
// process_example.c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>

int main() {
    pid_t pid = fork(); // Create a new process

    if (pid < 0) {
        // Fork failed
        perror("Fork failed");
        return 1;
    } else if (pid == 0) {
        // Child process
        printf("Child Process: My PID is %d, Parent PID is %d\n", getpid(), getppid());
    } else {
        // Parent process
        printf("Parent Process: My PID is %d, Child PID is %d\n", getpid(), pid);
    }

    return 0;
}
```

## Instructions to Run the Code:
### Steps 
1. Save the code in a file named process_example.c.
2. Open a terminal and navigate to the directory containing the file.
3. Compile the code using GCC:
    ``` gcc -o process_example process_example.c ```
4. Run the executable:
   ``` ./process_example```

### Expected Output
```csharp 
Parent Process: My PID is 12345, Child PID is 12346
Child Process: My PID is 12346, Parent PID is 12345
```



