# Understanding Processes vs Threads

## **Example: Thread Creation Using POSIX Threads (pthread)**
### This example demonstrates how to create a new thread using POSIX threads in C.

Code:

``` c
// thread_example.c
#include <stdio.h>
#include <pthread.h>

void* thread_function(void* arg) {
    printf("Thread: My thread ID is %lu\n", pthread_self());
    return NULL;
}

int main() {
    pthread_t thread_id;

    // Create a new thread
```
## Instructions to Run the Code:
### Steps 
1. **Save the code in a file named `thread_example.c.`**
2. **Open a terminal and navigate to the directory containing the file.**
3. **Compile the code using GCC and link the pthread library:**
    `bash 
    gcc -o thread_example thread_example.c -pthread
    `
4. **Run the executable:**
    `bash
    ./thread_example
    `
## Expetced Output

```mathematica
Thread: My thread ID is 140735240970112
Main Thread: Thread has finished execution
```

``
Note: The thread ID will vary each time you run the program.
``