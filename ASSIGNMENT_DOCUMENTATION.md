# Assignment 3 - Complete Documentation

**Student Name**: [Your Full Name]  
**Student ID**: [Your ID]  
**Date Submitted**: [Submission Date]

---

## 🎥 VIDEO DEMONSTRATION LINK (REQUIRED)

> **⚠️ IMPORTANT: This section is REQUIRED for grading!**
> 
> Upload your 3-5 minute video to your **PERSONAL Gmail Google Drive** (NOT university email).
> Set sharing to "Anyone with the link can view".
> Test the link in incognito/private mode before submitting.

**Video Link**: https://drive.google.com/file/d/1Gq8Ew6uJr-NrT8pyRTOwb8wOUJUtMog_/view?usp=sharing

**Video filename**: `444052883_Assignment3_Synchronization.mp4`

**Verification**:
- [ ] Link is accessible (tested in incognito mode)
- [ ] Video is 3-5 minutes long
- [ ] Video shows code walkthrough and commits
- [ ] Video has clear audio
- [ ] Uploaded to PERSONAL Gmail (not @std.psau.edu.sa)

---

## Part 1: Development Log (1 mark)

Document your development process with **minimum 3 entries** showing progression:

### Entry 1 - [26 April, 8:00 pm ]
**What I implemented**: 

 I forked the repository from GitHub, cloned it to my local machine, and updated my student ID in the code. I read the  assignment instructions. also quickly reviewed the project files to understand the basic structure.

**Challenges encountered**: 
There were no real challenges at this stage since the steps were similar to Assignment 1. The setup process was clear and straightforward.

**How I solved it**: 
I followed the instructions step by step in the README file and made sure all initial setup steps were completed correctly.

**Testing approach**: 
I checked that the repository was cloned successfully, the project opened in VS Code without issues, and the code compiled correctly after updating my student ID.

**Time spent**: 
About 10 minutes

---

### Entry 2 - [28 April, 9:00 pm]
**What I implemented**: 
I focused on learning the syntax of semaphores and mutex locks in Java. The lecture slides explained them using pseudocode, so I studied more to understand how to implement them in real Java code. I also learned where and how to use them in the program.

**Challenges encountered**: 
The main challenge was that the slides were written in pseudocode, which made it difficult to directly translate into Java syntax. I needed more time to understand the correct usage of Semaphore and ReentrantLock in Java.


**How I solved it**: 
I read the README file and i also read online resources to break down the syntax and understand how semaphores and locks work in Java. I also used an AI tool to get clearer explanations about the libraries and how they should be used in my assignment.

**Testing approach**: 
did small checks by reviewing example code and making sure I understood how acquire(), release(), lock(), and unlock() are used before applying them in the main project.

**Time spent**: 
About 35 minutes

---

### Entry 3 - [28 April, 9:45 pm]
**What I implemented**: 
Semaphore. Then I created four separate lock objects for the critical sections in the program.

At first, I was planning to use a single lock for all shared resources, but after thinking about it, I decided to use multiple locks instead. I chose this approach because it allows different threads to work in parallel on independent resources, which improves performance compared to using one global lock.

After that, I connected each lock with its corresponding shared resource to ensure proper protection of critical sections.

I also implemented the Semaphore. I noticed it was mainly used inside the Process class instead of SharedResources, so I applied it in the correct places where the CPU execution happens, based on the assignment requirements.

**Challenges encountered**: 
Understanding where exactly to place the Semaphore was a bit confusing at first, because it was not directly inside the shared resources class.

**How I solved it**: 
I solved the issue by accessing the Semaphore using an object reference

**Testing approach**: 
I did basic checks to make sure the code compiles and that locks and semaphores are placed in the correct sections.

**Time spent**: 
12 minutes
---

### Entry 4 - [28 April, 11:28PM]
**What I implemented**: 
Answered documentation questions (Part 2 to Part 6)

**Challenges encountered**: 
Making answers short but still correct

**How I solved it**: 
Read questions carefully and used my understanding of synchronization from the code

**Testing approach**: 
Checked answers against my implementation to make sure they match

**Time spent**: 
1 hour

---

### Entry 5 - [29 April, 8:00PM]
**What I implemented**: 
Recorded the video and completed the remaining questions.

**Challenges encountered**: 
Keeping the video within the 5-minute limit.

**How I solved it**: 
I trimmed unnecessary parts such as pauses and repetition using a video editing too

**Testing approach**: 
Reviewed the video to ensure clarity and that all required points were covered.

**Time spent**: 
30 minutes

---

## Part 2: Technical Questions (1 mark)

### Question 1: Race Conditions
**Q**: Identify and explain TWO race conditions in the original code. For each:
- What shared resource is affected?
- Why is concurrent access a problem?
- What incorrect behavior could occur?

**Your Answer**:

One race condition is in contextSwitchCount, which is shared by multiple threads. The problem is that  two threads can read and update it at the same time. This can cause lost updates and incorrect final values.

Another race condition is in executionLog, which is an ArrayList shared between threads. If multiple threads add data at the same time, it can cause missing entries 

---

### Question 2: Locks vs Semaphores
**Q**: Explain the difference between ReentrantLock and Semaphore. Where did you use each in your code and why?

**Your Answer**:

ReentrantLock is a binary lock used to protect critical sections so only one thread can access shared data at a time.
Semaphore is used to control how many threads can access a resource, so if it has 2 permits, only two threads can run at the same time and the rest will wait.


---

### Question 3: Deadlock Prevention
**Q**: What is deadlock? Explain TWO prevention techniques and what you did to prevent deadlocks in your code.

**Your Answer**:

Deadlock is a situation where threads get stuck waiting forever because each thread is holding a resource and waiting for another one held by a different thread.

One prevention technique is resource ordering (lock ordering), where resources are always acquired in a fixed order. In my code, I ensured that locks are used in a consistent way so threads do not create a circular waiting situation by requesting resources in different orders.

Another technique is using try-finally blocks, which ensures that locks are always released properly even if an error happens. This prevents threads from holding resources forever and reduces the chance of deadlock.

---

### Question 4: Lock Granularity Design Decision 
**Q**: For Task 1 (protecting the three counters), explain your lock design choice:
- Did you use ONE lock for all three counters (coarse-grained) OR separate locks for each counter (fine-grained)?
- Explain WHY you made this choice
- What are the trade-offs between the two approaches?
- Given that the three counters are independent, which approach provides better concurrency and why?

**Your Answer**:

I used fine-grained locking by assigning separate locks to each of the three counters because they are independent. This allows multiple threads to update different counters at the same time without blocking each other. The trade-off is more complexity compared to using one lock, but it improves performance. Coarse-grained locking is simpler but reduces concurrency because all threads must wait even if they access different counters. Since the counters do not depend on each other, fine-grained locking provides better concurrency and efficiency.

---

## Part 3: Synchronization Analysis (1 mark)

### Critical Section #1: Counter Variables

**Which variables**: 
contextSwitchCount, completedProcessCount, totalWaitingTime

**Why they need protection**: 
Because they are shared between multiple threads and updated at the same time, so without protection race conditions can happen and values become incorrect.

**Synchronization mechanism used**: 
ReentrantLock "fine-grained locks"

**Code snippet**:
```java
// Paste your implementation here
```

lockCts.lock();
try {
    contextSwitchCount++;
} finally {
    lockCts.unlock();
}

lockCmp.lock();
try {
    completedProcessCount++;
} finally {
    lockCmp.unlock();
}

lockAwt.lock();
try {
    totalWaitingTime += time;
} finally {
    lockAwt.unlock();
}

**Justification**: 
Each counter is independent, so I used separate locks to allow better concurrency. This prevents race conditions while still allowing multiple threads to work in parallel on different counters.

---

### Critical Section #2: Execution Log

**What resource**: 
executionLog (ArrayList)

**Why it needs protection**: 
Because multiple threads can add entries at the same time, and ArrayList is not thread-safe, which can cause missing data or runtime errors like ConcurrentModificationException.

**Synchronization mechanism used**: 
ReentrantLock

**Code snippet**:
```java
// Paste your implementation here
```
lockLge.lock();
try {
    executionLog.add(message);
} finally {
    lockLge.unlock();
}

**Justification**: 
The lock ensures only one thread can write to the log at a time, which keeps the execution history consistent and prevents data corruption.
---

### Critical Section #3: CPU Semaphore

**Purpose of semaphore**: 
To control how many processes can use the CPU at the same time and prevent uncontrolled concurrent execution.

**Number of permits and why**: 
1 permit, because I wanted only one process to execute in the CPU at a time (simulating a single CPU core).

**Where implemented**: 
In the Process class inside run() and runToCompletion() methods

**Code snippet**:
```java
// Paste your implementation here

SharedResources.cpuSemaphore.acquire();

try {
    // process execution code
} finally {
    SharedResources.cpuSemaphore.release();
}
```

**Effect on program behavior**: 
It ensures that only one thread enters the critical execution section at a time, preventing overlapping execution and making CPU scheduling behave correctly and predictably.
---

## Part 4: Testing and Verification (2 marks)

### Test 1: Consistency Check
**What I tested**: Running program multiple times to verify consistent results

**Testing procedure**: 
```bash
# Commands used (run the program at least 5 times)
javac SchedulerSimulationSync.java
java SchedulerSimulationSync
java SchedulerSimulationSync
java SchedulerSimulationSync
java SchedulerSimulationSync
java SchedulerSimulationSync
```

**Results**: 

I ran the program multiple times (5 runs in total). The results were consistent across all runs.
Total Context Switches: 31 in all runs
Total Completed Processes: 18 in all runs
Total log entries: 62 in all runs
Only minor differences appeared in waiting time values, which is expected due to thread scheduling timing, but the overall output structure remained the same.


**Why synchronization is necessary**: 
at the same time. This can cause race conditions such as lost increments in counters or corrupted ArrayList data. For example, contextSwitchCount++ is not atomic and could produce incorrect results without locks.

**Conclusion**: 

The implemented ReentrantLocks and Semaphore successfully prevented race conditions and ensured consistent and correct results across multiple executions.
---

### Test 2: Exception Testing
**What I tested**: Checking for ConcurrentModificationException

**Testing procedure**: 
javac SchedulerSimulationSync.java
java SchedulerSimulationSync

**Results**: 
No ConcurrentModificationException or any runtime errors were observed in any of the runs. The program executed successfully and the execution log was printed correctly each time.

**What this proves**: 
This proves that the executionLog ArrayList is properly protected using ReentrantLock, ensuring that only one thread modifies it at a time, which prevents concurrent modification issues and maintains data integrity.

---

### Test 3: Correctness Verification
**What I tested**: Verifying correct final values (total burst time, context switches, etc.)

**Expected values**: 
I expected the values to stay consistent across runs:

Same number of context switches
Same number of completed processes
Same number of log entries
Similar total waiting time (small differences allowed due to scheduling timing)

**Actual values**: 
Context Switches: 31
Completed Processes: 18
Total Log Entries: 62
Total Waiting Time: ~1202800ms – 1203400ms (small variation)

**Analysis**: 
The results are consistent across multiple runs, which proves that synchronization is working correctly. Even though waiting time slightly changes due to thread scheduling and timing, all shared counters and logs remain stable. This shows that locks and semaphores successfully prevent race conditions and ensure correct final values.

---

### Test 4: Different Scenarios
**Scenario tested**: [e.g., different time quantum, more processes, etc.]
Scenario tested: I ran the program with different inputs (different number of processes and different time quantum values).

**Purpose**: 
To check how the scheduler behaves under different workloads and to verify that synchronization still works correctly in all cases.

**Results**: 
In all scenarios, the program still produced correct and consistent results. The values for context switches, completed processes, and log entries remained stable, while waiting time changed depending on the workload.

**What I learned**: 
Synchronization works correctly regardless of the number of processes or time quantum. I also learned that increasing processes increases scheduling activity (more context switches and logs), while changing time quantum affects how long each process runs per cycle.

---

## Part 5: Reflection and Learning

### What I learned about synchronization:

I learned that synchronization controls how multiple threads access shared resources to prevent errors. Without it, race conditions can occur and lead to incorrect results. I used ReentrantLock to protect critical sections and Semaphore to control CPU access. One challenge was choosing between a single lock or multiple locks. I chose multiple locks to improve concurrency. Overall, I learned how to balance performance and correctness in multithreading.

---

### Real-world applications:

Give TWO examples where synchronization is critical:

**Example 1**: 
Bank systems to prevent wrong balance updates when multiple transactions happen

**Example 2**: 
Ticket booking systems to avoid multiple users booking the same seat

---

### How I would explain synchronization to others:

[Explain to someone who just finished Assignment 1 - use simple terms and analogies]
Synchronization is like a turn system where threads take turns and wait. The way it is organized depends on the program.

---

## Part 6: GitHub Repository Information

**Repository URL**: 
https://github.com/HasanMaarouf883/OS-Assignment3-Hasan-Maarouf

**Number of commits**: 
5

**Commit messages**: 
1. Set my student ID: 444052883
2. mutex lock
3. Semaphore
4. documentation questions (Part 2 to Part 6)
5. Assignment completed

---

## Summary

**Total time spent on assignment**: 
about 2 days

**Key takeaways**: 
1. I learned how to apply synchronization in real code using locks and semaphores.
2. I understood the difference between using a single lock for multiple critical sections versus separate locks, and how each approach affects concurrency and performance.

3. I learned that synchronization improves program correctness by preventing race conditions in multithreaded programs.

**Most challenging aspect**: 
The most challenging aspect was implementing the code correctly because the syntax was new and it was sometimes difficult to decide where to apply synchronization mechanisms.

**What I'm most proud of**: 
I am most proud of successfully implementing synchronization and achieving correct and consistent results.

---

**End of Documentation**
