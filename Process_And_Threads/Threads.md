# Understanding Processes vs Threads

## **Example: Thread Creation Using POSIX Threads (pthread)**
## This example demonstrates how to create a new thread using POSIX threads in C.

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
    if (pthread_create(&thread_id, NULL, thread_function, NULL) != 0) {
        perror("Thread creation failed");
        return 1;
    }

    // Wait for the thread to finish
    if (pthread_join(thread_id, NULL) != 0) {
        perror("Thread join failed");
        return 1;
    }

    printf("Main Thread: Thread has finished execution\n");
    return 0;
}
```

## Instructions to Run the Code:
Save the code in a file named thread_example.c.
Open a terminal and navigate to the directory containing the file.
Compile the code using GCC and link the pthread library:
bash
Copy code
gcc -o thread_example thread_example.c -pthread
Run the executable:
bash
Copy code
./thread_example
Expected Output:
mathematica
Copy code
Thread: My thread ID is 140735240970112
Main Thread: Thread has finished execution