# Basics of Multithreading in C (Using `pthread`)

## **Example: Creating Multiple Threads and Passing Arguments**

This example creates multiple threads and passes a unique number to each thread.

## Code:
```c
// multithread_example.c
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>

#define NUM_THREADS 3

void* thread_function(void* arg) {
    int thread_num = *((int*)arg);
    printf("Thread %d: My thread ID is %lu\n", thread_num, pthread_self());
    free(arg); // Free the allocated memory
    return NULL;
}

int main() {
    pthread_t threads[NUM_THREADS];

    for (int i = 0; i < NUM_THREADS; i++) {
        int* thread_num = malloc(sizeof(int));
        if (thread_num == NULL) {
            perror("Failed to allocate memory");
            return 1;
        }
        *thread_num = i + 1;

        // Create a new thread
        if (pthread_create(&threads[i], NULL, thread_function, thread_num) != 0) {
            perror("Thread creation failed");
            free(thread_num);
            return 1;
        }
    }

    // Wait for all threads to finish
    for (int i = 0; i < NUM_THREADS; i++) {
        if (pthread_join(threads[i], NULL) != 0) {
            perror("Thread join failed");
            return 1;
        }
    }

    printf("Main Thread: All threads have finished execution\n");
    return 0;
}
```

## Instructions to Run the Code:

### Steps
1. Save the code in a file named multithread_example.c.
2. Open a terminal and navigate to the directory containing the file.
3. Compile the code using GCC and link the pthread library:

```bash
gcc -o multithread_example multithread_example.c -pthread
```
2. Run the executable:
```bash
./multithread_example
```
## Expected Output
```csharp
Thread 1: My thread ID is 140638348838656
Thread 2: My thread ID is 140638340445952
Thread 3: My thread ID is 140638332053248
Main Thread: All threads have finished execution
```
**Note: The order and thread IDs may vary due to concurrent execution.**