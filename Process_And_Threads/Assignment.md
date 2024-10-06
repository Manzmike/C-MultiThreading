# Understanding Processes vs Threads

## Assignment: Creating Multiple Child Processes and Threads

### This assignment requires you to create multiple child processes and threads to deepen your understanding of process and thread creation in C.

## Task Description
### Process Assignment:
- Write a C program that creates three child processes using fork().
- Each child process should print its own PID and its parent's PID.
- The parent process should wait for all child processes to finish before exiting.
- Thread Assignment:
- Write a C program that creates three threads using POSIX threads.
- Each thread should print a message along with its thread ID.
- The main thread should wait for all threads to finish before exiting.

### Instructions:
- Process Assignment Steps
- Create a new C file named multi_process.c.
- Use a loop or multiple fork() calls to create three child processes.
- In each child process, print the child's PID and its parent's PID.
- In the parent process, wait for all child processes to finish using wait() or waitpid().
- Compile and run your program to verify it works as expected.
- Thread Assignment Steps
- Create a new C file named multi_thread.c.
- Use a loop to create three threads using pthread_create().
- In each thread, print a message along with the thread's ID.
- In the main thread, wait for all threads to finish using pthread_join().
- Compile and run your program to verify it works as expected.


## Expected Output
**For the process assignment:**

``` csharp
Copy code
Child Process 1: My PID is 12346, Parent PID is 12345
Child Process 2: My PID is 12347, Parent PID is 12345
Child Process 3: My PID is 12348, Parent PID is 12345
Parent Process: My PID is 12345, All child processes have finished.
```
**For the thread assignment:**
```csharp
Copy code
Thread 1: My thread ID is 140735240970112
Thread 2: My thread ID is 140735232577408
Thread 3: My thread ID is 140735224184704
Main Thread: All threads have finished execution
Note: The PID and thread ID numbers will vary each time you run the program.```