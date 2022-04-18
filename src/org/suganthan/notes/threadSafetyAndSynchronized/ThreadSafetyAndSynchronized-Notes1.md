Thread Safety & Synchronized:
=============================

Thread Safe:
============

    A class and its public APIs are labelled as thread safe if multiple threads can consume the exposed APIs without
    causing race conditions or state corruption for the class. Note that the composition of two or more thread-safe classes
    doesn't guarantee the resulting type to be thread-safe.

Synchronized:
=============

    It can used to restrict access to critical sections one thread at a time.

    Each object in Java has an entity associate with it called "Monitor Lock" or just Monitor. Think of it as an
    exclusive lock. Once a thread gets hold of the monitor of an object, it has exclusive access to all the methods
    marked as synchronized. No other threads will be allowed to invoke a method on the object that is marked as
    synchronized and will block, till the first thread releases the monitor which is equivalent of the first thread
    exiting the synchronized method.

    Note carefully:

        1. For static method: the monitor will be class object, which is distinct from the monitor for each instance of the same class.
        2. If an uncaught exception occurs in a synchronized method, the monitor is still released.
        3. Futhermore, synchronized blocks can re-entered.

        class Employee {
            //Shared variable
            String name;

            //method is synchronized on `this` object
            public synchronized void setName(String name) {
                this.name = name;
            }

            //also synchronized on the same object.
            public synchronized void resetName() {
                this.name = "";
            }

            //equivalent of adding synchronized in method definition
            public void getName() {
                synchronized(this) {
                    return this.name;
                }
            }
        }

        In the above class, if we create an object and thread different threads attempted to execute a each method
        of the object, only one will get access, and the other two will block.

        Refer to ThreadSafetyExample.java

        If we synchronized on a different object other than the this object, which is only possible for the getName method
        given the way we have written the code, the critical section of the program become protected by two differnt locks.
        In tat scenario, since setName and resetName would have been synchronized on `this` object only one of two methods
        could be executed concurrently. However, getName would be synchronized independently of the other two
        methods and can be executed alongside one of them.

        Refer to ThreadSafetyWithTwoObjectsExample.java

        With synchronized keyword, Java forces you to implicitly acquire and release the monitor-lock for the object with the same method.

        One can't explicitly acquire and release the monitor in different method.

        Here, the same thread will acquire and release the monitor!!!
        In Semaphore we could acquire and release monitor in different methods or by different threads.
