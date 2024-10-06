
---

### **File 2: `assignment_topic_1.md`**


# Topic 1: Understanding Processes vs Threads

## Assignment: Creating Multiple Child Processes and Threads

### Task Description

1. **Process Assignment:**

   - Write a C program that creates **three child processes** using `fork()`.
   - Each child process should print its own PID and its parent's PID.
   - The parent process should wait for all child processes to finish before exiting.

2. **Thread Assignment:**

   - Write a C program that creates **three threads** using POSIX threads.
   - Each thread should print a message along with its thread ID.
   - The main thread should wait for all threads to finish before exiting.

### Instructions

- **Understand the Example Codes** provided in `example_topic_1.md` to help you with this assignment.
- **Requirements:**
  - Use proper error checking after creating processes or threads.
  - Ensure that the output clearly indicates which process or thread is executing.
- **Hints:**
  - For processes, you may need to call `fork()` multiple times or use a loop.
  - For threads, consider using an array of `pthread_t` variables and a loop to create and join threads.

### Submission

- Submit two C files:
  - `multi_process.c` for the process assignment.
  - `multi_thread.c` for the thread assignment.
- Include comments in your code to explain your logic.
