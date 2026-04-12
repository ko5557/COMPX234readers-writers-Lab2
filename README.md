Readers-Writers Problem
Name: Deng ZiChen
ID: 20243006955

1. Project overview
This project implements a monitor-style solution for the classic Readers-Writers problem in python. The solution uses threading.Condition to safely synchronize access to a shared resource, folling these rules:
a. Multiple readers can read concurrently when no writer is active.
b. Writers require exclusive access, only one writer at a time.
c. Readers and writers cannot run at the same time.

2. Implementation Design
The core component is the ReadersWritersMonitor class, which acts as a monitor to protect shared state:
a. active_readers: counts how many readers are currently reading
b. active_writers: indicates whether a writer is writing(0 or 1)
c. waiting_writers: optional counter for waiting writers
2.2 Synchronization Logic
a. start_read(): Waits if a writer is active, then increments the reader count.
b. end_read(): Decrements the reader count; wakes waiting threads if no readers remain.
c. start_write(): Waits until no readers or writers are active, then marks the writer as active.
d. end_write(): Marks the writer as inactive and wakes all waiting threads.
All shared state is protected inside the monitor using threading.Condition. All waits use while loops to recheck conditions after wakeup.

3. How to Run the Program
Ensure you have Python 3 installed.
Run the program using:
python readers_writers.py

## 4. Sample output
Reader 2 wants to read
Reader 2 staarts reading. Active readers = 1
Reader 2 is READING
Reader 3 wants to read
Reader 3 staarts reading. Active readers = 2
Reader 3 is READING
Writer 1 wants to write
Reader 1 wants to read
Reader 1 staarts reading. Active readers = 3
Reader 1 is READING
Writer 2 wants to write
Reader 2 ends reading. Active readers = 2
Reader 2 finished reading
Reader 1 ends reading. Active readers = 1
Reader 1 finished reading
Reader 1 wants to read
Reader 1 staarts reading. Active readers = 2
Reader 1 is READING
Reader 3 ends reading. Active readers = 1
Reader 3 finished reading
Reader 2 wants to read
Reader 2 staarts reading. Active readers = 2
Reader 2 is READING
Reader 1 ends reading. Active readers = 1
Reader 1 finished reading
Reader 3 wants to read
Reader 3 staarts reading. Active readers = 2
Reader 3 is READING
Reader 2 ends reading. Active readers = 1
Reader 2 finished reading
Reader 1 wants to read
Reader 1 staarts reading. Active readers = 2
Reader 1 is READING
Reader 2 wants to read
Reader 2 staarts reading. Active readers = 3
Reader 2 is READING
Reader 1 ends reading. Active readers = 2
Reader 1 finished reading
Reader 3 ends reading. Active readers = 1
Reader 3 finished reading
Reader 2 ends reading. Active readers = 0
Reader 2 finished reading
Writer 1 start write. Active writers = 1
Writer 1 is WRITING
Reader 3 wants to read
Writer 1 end write. Active writers = 0
Writer 1 finished writingReader 3 staarts reading. Active readers = 1

Reader 3 is READING
Reader 3 ends reading. Active readers = 0
Reader 3 finished reading
Writer 2 start write. Active writers = 1
Writer 2 is WRITING
Writer 1 wants to write
Writer 2 end write. Active writers = 0
Writer 2 finished writing
Writer 1 start write. Active writers = 1
Writer 1 is WRITING
Writer 2 wants to write
Writer 1 end write. Active writers = 0
Writer 1 finished writingWriter 2 start write. Active writers = 1
Writer 2 is WRITING

Writer 2 end write. Active writers = 0
Writer 2 finished writing
READERS-WRITERS SIMULATION DONE !

[Done] exited with code=0 in 5.72 seconds
##
