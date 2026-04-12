1. Project overview
This project implements a monitor-style solution for the classic Readers-Writers problem in python. The solution uses threading.Condition to safely synchronize access to a shared resource, folling these rules:
a. Multiple readers can read concurrently when no writer is active.
b. Writers require exclusive access, only one writer at a time.
c. Readers and writers cannot run at the same time.
