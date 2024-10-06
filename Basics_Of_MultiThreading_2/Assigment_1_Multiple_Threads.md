# Assignment: Summing an Array Using Multiple Threads

This assignment requires you to calculate the sum of an array of integers using multiple threads.

## Task Description
### **Objective: Write a C program that calculates the sum of an array of integers using multiple threads.**
Array Details: The array should contain 20 integers.
Thread Details: Use 4 threads to compute the sum.
Functionality:
Each thread should calculate the sum of a portion of the array (i.e., 5 integers per thread).
The main thread should collect the partial sums from each thread and compute the total sum.

## Instructions:
### Steps

#### Create a New C File:
2. Create a new C file named ```array_sum.c.```
3. Initialize the Array:
4. Initialize an array with 20 integers. You can choose any values you like or generate them programmatically.
#### Divide the Array:
5. Split the array into 4 equal parts, each containing 5 integers.
6. Create a Structure for Thread Arguments:
7. Define a structure to pass the array portion and its size to the thread function.
```c
typedef struct {
    int* array;
    int size;
    long partial_sum;
} thread_data_t;
```
8. Implement the Thread Function:
9. In the thread function, calculate the sum of the assigned portion of the array.
10. Store the partial sum in the partial_sum field of the structure.
```c
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
11. In the main function, create 4 threads, each responsible for summing a portion of the array.
12. Pass the relevant portion of the array and its size to each thread.
13. Collect Partial Sums and Compute Total Sum:
14. After all threads have completed, collect the partial_sum from each thread's data structure.
15. Compute the total sum by adding up all partial sums.
16. Print the total sum.
#### Compile and Run the Program:
18. Compile the program using GCC and link the pthread library:
```bash
gcc -o array_sum array_sum.c -pthread
```
#### Run the executable:
```bash
./array_sum
```
### Example Code Skeleton
```c
// array_sum.c
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>

#define ARRAY_SIZE 20
#define NUM_THREADS 4

typedef struct {
    int* array;
    int size;
    long partial_sum;
} thread_data_t;

void* sum_array(void* arg) {
    thread_data_t* data = (thread_data_t*)arg;
    data->partial_sum = 0;
    for (int i = 0; i < data->size; i++) {
        data->partial_sum += data->array[i];
    }
    pthread_exit(NULL);
}

int main() {
    int array[ARRAY_SIZE] = { /* Initialize with 20 integers */ };
    pthread_t threads[NUM_THREADS];
    thread_data_t thread_data[NUM_THREADS];
    int portion_size = ARRAY_SIZE / NUM_THREADS;
    long total_sum = 0;

    // Initialize and create threads
    for (int i = 0; i < NUM_THREADS; i++) {
        thread_data[i].array = &array[i * portion_size];
        thread_data[i].size = portion_size;
        thread_data[i].partial_sum = 0;
        if (pthread_create(&threads[i], NULL, sum_array, (void*)&thread_data[i]) != 0) {
            perror("Thread creation failed");
            return 1;
        }
    }

    // Wait for threads to finish and collect partial sums
    for (int i = 0; i < NUM_THREADS; i++) {
        if (pthread_join(threads[i], NULL) != 0) {
            perror("Thread join failed");
            return 1;
        }
        printf("Partial Sum from Thread %d: %ld\n", i + 1, thread_data[i].partial_sum);
        total_sum += thread_data[i].partial_sum;
    }

    printf("Total Sum: %ld\n", total_sum);
    return 0;
}
```
### Expected Output
```csharp
Partial Sum from Thread 1: X
Partial Sum from Thread 2: Y
Partial Sum from Thread 3: Z
Partial Sum from Thread 4: W
Total Sum: N
Replace X, Y, Z, W with the actual partial sums and N with the total sum.
```