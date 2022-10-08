**Deadlock**: Deadlock occurs when two or more threads aren't able to make any progress because the resource requried by the
first thread is held by the second and resource required by the second thread is held by the first.

**Liveness**: Ability of a program or an application to execute in a timely manner is called liveness.

**Live-Lock**: The live-lock occurs when two threads continuously react in response to the action by the other thread without
making any real progress.

**Dead lock example**

    void increment() {
        acquire MUTEX_A
        acquire MUTEX_B
        //do work here
        release MUTEX_B
        release MUTEX_A
    }

    void decrement() {
        acquire MUTEX_B
        acquire MUTEX_A
        //do work here
        release MUTEX_A
        release MUTEX_B
    }

    T1 enters function increment

    T1 acquires MUTEX_A

    T1 gets context switched by the operating system

    T2 enters function decrement

    T2 acquires MUTEX_B

    both threads are blocked now

**Reentrant Lock**
    Re-entrant Locks allow for re-locking or re-entering of the synchronization lock.