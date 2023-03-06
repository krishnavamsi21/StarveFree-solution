# StarveFree-solution
StraveFree Readers Writers Solution
# Reader's problem 
There is a semaphore for both readers and writers called rwmutex.
Whichever process acquires this mutex first, undergoes execution first, i.e they follow fcfs(first come first serve) method.
While the readers process have this semaphore(rwmutex), writers cannot enter the critical section, and vice versa (while a writer is having this semaphore, readers cannot enter the critical section).
Two or more readers can read simaltaneously because the rwmutex is only used in the readcnt updating part(we know that only one reader can update readcnt at a time), but not in the //reading part.
There is a semaphore for readers called mutex.
This is used for updating the readcount semaphore called readcnt, which indicates the number of readers reading the critical section at a particular time.
There is a semaphore called wrt, for writers which is used such that no other writer can write while one writer is writing in the critical section.

# Writer's problem
There is a semaphore called rwmutex which is acquired by the process in the fcfs order for accessing the critical section and no other processes access the critical section while the process having rwmutex semaphore is accessing the critical section.
There is a semaphore called wrt which is used by writer process so that no other writer process write while it is writing in the critical section.

# Let's take an example.
Let's assume arrival of 4 readers and 1 writer in the order RRWRR.

As a reader has arrived first, it acquires the rwmutex semaphore(so that no writer could enter now), the mutex semaphore(so that no other reader could update readcnt now) and updates readcnt, signals both the semaphores and starts reading.
While the first reader has entered, the wrt mutex is waited by reader so that writer process cannot write until the readers that have arrived before writer in the order has completed reading.
Second reader also acquires rwmutex semaphore, mutex semaphore and updates readcnt, signals both the semaphores and starts reading.
When both the readers have completed their reading, they signal the wrt semaphore.
As in the order , next one is writer, it acquires the rwmutex, and doesn't allow the next readers to enter the critical section until writer completes its writing part, as it has arrived first.
Writer can only start writing when the readers before have signaled the wrt semaphore.
After completing writing part, the writer signals the rwmutex semaphore so that the next processes can start their execution.
The next readers in the order start their reading process now by acquiring the rwmutex semaphore, mutex semaphore, updating reacnt, signal out both the semaphore and complete reading.
