# Basics of Multithreading in C (Using pthread)

## Assignment: Summing an Array Using Multiple Threads

This assignment requires you to calculate the sum of an array of integers using multiple threads.

## Task Description
### Objective: Write a C program that calculates the sum of an array of integers using multiple threads.
Array Details: The array should contain 20 integers.
Thread Details: Use 4 threads to compute the sum.
Functionality:
Each thread should calculate the sum of a portion of the array (i.e., 5 integers per thread).
The main thread should collect the partial sums from each thread and compute the total sum.
##  Instructions:
### Steps

#### Create a New C File:
1. Create a new C file named array_sum.c.
2. Initialize the Array:
3. Initialize an array with 20 integers. You can choose any values you like or generate them programmatically.
```c
int array[20] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10,
                 11, 12, 13, 14, 15, 16, 17, 18, 19, 20};
``` 
#### Divide the Array:
4. Split the array into 4 equal parts, each containing 5 integers.
5. Create a Structure for Thread Arguments:
6. Define a structure to pass the array portion and its size to the thread function.
```c
Copy code
typedef struct {
    int* array;
    int size;
    long partial_sum;
} thread_data_t;
```
#### Implement the Thread Function:
7. In the thread function, calculate the sum of the assigned portion of the array.
8. Store the partial sum in the partial_sum field of the structure.
```c
Copy code
void* sum_array(void* arg) {
    thread_data_t* data = (thread_data_t*)arg;
    data->partial_sum = 0;
    for (int i = 0; i < data->size; i++) {
        data->partial_sum += data->array[i];
    }
    pthread_exit(NULL);
}
```
#### Create and Launch Threads:
9. In the main function, create 4 threads, each responsible for summing a portion of the array.
10. Pass the relevant portion of the array and its size to each thread.
```c
for (int i = 0; i < NUM_THREADS; i++) {
    thread_data[i].array = &array[i * portion_size];
    thread_data[i].size = portion_size;
    thread_data[i].partial_sum = 0;
    if (pthread_create(&threads[i], NULL, sum_array, (void*)&thread_data[i]) != 0) {
        perror("Thread creation failed");
        return 1;
    }
}
```
#### Collect Partial Sums and Compute Total Sum:
11. After all threads have completed, collect the partial_sum from each thread's data structure.
12. Compute the total sum by adding up all partial sums.
13. Print the total sum.
```c
for (int i = 0; i < NUM_THREADS; i++) {
    if (pthread_join(threads[i], NULL) != 0) {
        perror("Thread join failed");
        return 1;
    }
    printf("Partial Sum from Thread %d: %ld\n", i + 1, thread_data[i].partial_sum);
    total_sum += thread_data[i].partial_sum;
}
printf("Total Sum: %ld\n", total_sum);
```

#### Compile and Run the Program:
14. Compile the program using GCC and link the pthread library:
```
bash
gcc -o array_sum array_sum.c -pthread
```
#### Run the executable:
```bash
./array_sum
```
### Example Output
```csharp
Copy code
Partial Sum from Thread 1: 15
Partial Sum from Thread 2: 40
Partial Sum from Thread 3: 65
Partial Sum from Thread 4: 90
Total Sum: 210
```
**Note: The actual partial sums and total sum will depend on the values in your array.**

# Basics of Multithreading in C (Using pthread)

## Example: Creating Multiple Threads and Passing Arguments

This example creates multiple threads and passes a unique number to each thread.

Code:

```c
Copy code
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


### Instructions to Run the Code:
#### Steps
1. Save the code in a file named multithread_example.c.
2. Open a terminal and navigate to the directory containing the file.
3. Compile the code using GCC and link the pthread library:
```bash
gcc -o multithread_example multithread_example.c -pthread
```
Run the executable:
```bash
./multithread_example
```
#### Expected Output
```csharp
Thread 1: My thread ID is 140638348838656
Thread 2: My thread ID is 140638340445952
Thread 3: My thread ID is 140638332053248
Main Thread: All threads have finished execution
```
**Note: The order and thread IDs may vary due to concurrent execution.**