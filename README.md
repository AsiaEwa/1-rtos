# 1-rtos: concurrent programming-RTOS: processes and threads POSIX
## 2.
The update threads() function updates threads in real time while a program is running on Linux.

## 3.
### Preview of system operation while the process is running:
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/fb55a0a8-b5e2-409a-bc21-b46466945776)

By running via console commands:
pwd – printing the path to the current directory, shows the one we are in
ls – listing the contents of the directory (l-detailed information, s-sorting by size)
cd PWiSCR/Threads/Debug/ - move to the specified directory: syntax cd - path
sudo ./Threads – runs the Threads directory as root
and then, while the running program is running, analyzing the behavior of the threads and the system by calling the commands:
ps –e (ps is checking, display process, e all processes)
ps –cT –p [PID number] (c-resume, T- timeout n seconds, p - downloading the content of pages with attachments) Program result:
The values of var 1 and var 2 depend on the priority given to them by the process algorithm u in the code.
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/50360c2a-0213-4147-91d2-743ba81d94e9)

CLS - name of the algorithm, PRI - priority value, TTY - identifier, terminal name of the running process, CMD - name of the file from which the process was created
With the original FIFO algorithm var1=var2, the values are equal:
From the console result, you can read the PID numbers of individual threads, their scheduling algorithms, priorities, identifiers of the terminal on which the process was started, the amount of processor time used for a given process (time) and the name of the file from which the process was created.
By reading e.g. no. PID:4797, FIFO algorithm, priority 60, time 19s, cmd, i.e. file: Threads.
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/4495623a-02e2-47d9-8d51-5dc210ba60b2)

With the top -H command, we open a window in the console with information about the computer's operating time, user, working threads, sleep, etc. This allows us to obtain information about processes sorted according to CPU usage time.
The white line provides information about the process PID, user, priority, [Ni] the value of the nice parameter, [VIRT] the total size of virtual memory used by the process, [RES] the size of the resident memory (not exchangeable in KB), [SRH] the size of the area shared memory used by the process, [S] process state: [S] - sleeping, [R] - running, [D] - unideruptable running, [Z] - zombie, [T] – traced or stopped, [%CPU] – CPU time usage in %; [%MEM] - physical memory usage in %; [Time] – accumulated processor time used since the start of the process, [command] – process name.
You can also use the ps -1 command to control process priorities, but top -H is better. Process priority tells the operating system how to allocate CPU time to a process.
SPID is a PID marked with "S" sorted by number sequentially
Thread marked CLS
The first line of the base thread 2003 TS usually has a different, more important priority than the next ones, here it has a priority value of 19. The next one (the correct one being checked) with the number 2003 FF has a priority value of 60

## 4.
### Preview of system operation while the process is running:
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/2ddbff1d-9170-4d15-a4e9-c8c7798c8006)

There are no threads created except the one associated with the OTHER process, which is not a real-time thread marked with the symbol TS. You can manipulate the change in the algorithm, and therefore its priority. This is done with the sudo chrt –r –p command. An example of changing the algorithm in the console from Other to Round Robin.
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/d2cd81ed-6a30-4b7c-b41a-dd0dbd7c0d02)

There are no threads running, hence the entry Tasks, not Threads. The program does not work with threads. Result on startup:
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/425c5aa2-c7b1-4f33-8458-735f1da1b69c)

#### After completing the activities:
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/843bd251-11e0-47f1-a2db-5d87d154bec5)

a) It is possible to manipulate the parameters of the running process. This can be done using system tools by changing the priority value and changing the scheduling algorithm (FIFO, RR, OTHER). Individual changes are made to the code, then compiled, and then the operation of the introduced modification in relation to the system is checked one by one.

b) If there is no such process for the thread, it means that it has not been started because no threads have been created. Read values:
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/bfe0fa3c-63be-44ec-8f69-811d0d3eb835)
no priority
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/a8d484cc-0b7c-439d-9d98-e775ba76cdcd)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/bd05f11d-99a1-4f5f-a9d3-7dc276749117)

## 5.
With priority 10 (With the priority set in the environment code, 20, the console returned the value 60, while with the value 10, the console responds with the value 50, correctly, 10 lower) FIFO
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/c3e5162e-0e93-412d-a249-97c5d4cbd273)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/8f274272-645d-4fa2-a0bb-435517ad2650)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/dd2805db-6e1d-4283-a682-af3e1d091cee)
Round-Robin algorithm
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/d63b15c6-e3eb-4224-8835-82f670b69422)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/c56d24e3-de88-415c-a5a6-56fb71a7d9d5)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/1e1099f8-63d0-4b1e-be3a-8e223a005588)

There are different var 1 and var 2
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/d1ecebbe-f3a4-460d-a2e8-1fcf1a359d33)

From the generated data below, we can read the algorithm noted in the CLS column, e.g. FIFO and the thread priority of 60. You can also see the time taken by the machine to work on the thread.

c) the process that creates 1 thread has no problem with scheduling what has to be done first, because it is alone, has shorter code and shorter work time, which can theoretically be done immediately, taking up less memory.

d) By entering the command sudo chrt –r –p 10 1643, where 1643 is the PIDU number, the FIFO scheduling algorithm was changed to Round-robin RR straight from the console, without the need to enter it in the code.

## 6.
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/beabc42f-9f02-47bb-9641-c332650da97c)

For the Round Robin algorithm, different values of var 1 and var 2 are observed during operation:
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/790c563b-d86a-4bb1-92f4-fb4bca5c7093)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/c4090f12-ff50-4ef3-8926-4cb5ad5847a2)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/c229f930-c409-4c44-b472-4aed77f1f29d)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/06c65ab8-829a-4172-b3e9-88368de46298)

For the FIFO algorithm
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/70040af4-b984-4d3c-b456-e6e69091067e)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/c7bef1a1-6658-4ebb-90c8-0d1f0daed857)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/53f28085-ebb4-458a-91f1-17b343c48943)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/9ef93bc1-3a0a-4019-b2e2-548727a73339)

When checking the same steps for the second time: different var 1 and var 2 occur during operation:
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/3dc993ee-e56a-476d-b1dd-f3fd45357aa4)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/e121fa35-d6b4-44b8-87a8-d25a05aa2ab4)

10 threads with the same priority of 60 at the same time except the first thread.
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/c9027a38-7777-46de-bbf5-b41235dd0a7d)

FIFO: same as above
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/03b475c0-0a65-4c58-981a-0981e5f33941)

But throughout the code, var1 and var2 have equal values in the FIFO scheduling algorithm
Priorities and time except one, probably due to launching after a long break
c,d) 
#### Operating status: normal without delay and with sleep delay
The average CPU load and other data about system operation can be obtained using the uptime command, which provides the current time, how long the computer has been working, how many users are logged in, and the load over the last minute, 5 minutes, 15 minutes. The average number of processes waiting to be executed per unit of time. In a situation where we have 1 processor with 1 core, the limit value is
processes were running without waiting is 1. If this value increases, the processor is overloaded. (A queue of activities is created or, in case of particular excess, a suspension occurs). (If the processor has 4 cores, the limit is 4, it is possible to perform more actions at the same time without waiting).
The data posted is with the top function because it shows more information than uptime:
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/cde478df-7b97-4cdb-b85a-f5f7f8ebc7bb)

normal throw (to compare with the sleep throw, next one below):
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/fd9d3e23-56af-4215-9070-110110613a3c)

After enabling Nano Sleep 1000msec:
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/12668297-b3bf-435c-a776-091e97e7f80b)

#### There have been some changes:
- threads have been put to sleep (to be executed by the system, visible on the top of the second line are Tasks - tasks, not Threads - threads)
- the processor consumes much more time than traditionally, without the use of nanosleep
- higher state of the sleep process
Less memory usage
-almost twice as much cache file buffering
-significantly lower free memory consumption

#### Further comparison with different nanosleep values for: 
100msec:
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/465bc359-ed40-43e8-b02c-8f7582c86f42)

1 msec:
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/e97f57c6-d889-40b6-82e7-25dde03222fc)

#### Compare actions between different sleep time values using nanosleep code:
-The smaller the time value, the smaller changes in the size of no are visible
-The shorter the time, the fewer Tasks and the less running work
- Longer CPU sleep state.
- Slight increase in free and used memory usage. Slightly reduced buffering/cache.
Shorter operating times of running processes, including threads.
nanosleep() - high-resolution sleep, suspends the execution of the calling thread until at least the time specified in * req has elapsed, or a signal has been provided that triggers a handler call to the calling thread or terminating the process.
The timespec structure is used to specify time intervals with nanosecond precision. It is defined as follows:
struct timespec {
time_t tv_sec; /* seconds */
long tv_nsec; /*nanoseconds*/
};

The value of the nanoseconds field must be between 0 and 999999999. nanosleep() provides a higher resolution for specifying the sleep interval format; makes the task of resuming sleep that was interrupted by signal handling easier
With the same scheduling algorithm, the same occurs: priority 50, FIFO algorithm, equal time, except for the first thread, probably after a long break of inactivity the startup process required more time.
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/f9eb1835-d532-4e4c-8dc3-c5bbad97b82f)

## 7.
For different scheduling algorithms, different scheduling values can be observed, and the running time also changes
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/f77ffd58-8a57-4fe1-a4a5-272e84aba5d4)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/eb85201e-6c24-4cd3-939b-9021011a37fc)

The state of 3 different threads with different scheduling algorithms, different priority values and different runtimes.
The Round-robin algorithm can be described as medium in terms of priority, but it executes in one of the shortest times. The so-called FIFO algorithm queue, has a higher priority value.
The Round Robin scheduling algorithm is time-dependent, it comes before the FIFO algorithm, which in this case follows it according to the next value of priority and time. The RR process has a shorter running time than FIFO, it is "faster".
Same priority algorithm and similar time (first different, probably due to startup delay). The values of var 1 and var 2 are not equal, but they have the same priority, different algorithm and time. The time is the same for the same scheduling algorithm.
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/b41238bb-70d3-48b6-a5ae-2f45abe2671d)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/f8933c94-53ea-4956-ba94-4f75a093c576)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/9b101e9f-2f35-47b2-93c5-f3055750277b)

### SUMMARY
The thread priority determines its execution along with the given algorithm written in the code. The execution time depends on the adopted rhythm algorithm method and the number of threads. Method:

SCHED_RR: the process gets the CPU for the time quantum stored in its task_struct in the counter field. After this time quantum has elapsed, the processor is dispossessed and the process scheduling algorithm is launched.

SCHED_FIFO: The process receives the processor until it frees it or a process from the conceptual queue with a higher number appears. When a more privileged process appears, the processor is taken away from the process and it is placed at the beginning of the process queue, so that when processes from higher queue numbers finish requesting the processor, the process that was previously executing is selected.

The sudo chrt –r – p 10 command (PID number) allows you to change the scheduling algorithm.
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/ec8fb7a4-206c-4073-9d95-d6efd9c599c5)

#### Tags (signs): 
sudo – root, chrt - manipulate process attributes in real time
R - number of processes in the runable state (executing or ready) p - downloading the content of pages with attachments p as pid and enter its number (if you give something else, e.g. -f, it means changing the policy to FIFO and if -r - to Round- robin, -o other)
When changing the scheduling algorithm of the first TS other thread to RoundRobin, its priority changed but the time remained the same. Typically, initial threads may have larger startup time values. (time displayed in the second line)
![image](https://github.com/AsiaEwa/1-rtos/assets/101841759/c1f4d565-a9ec-42ce-b90f-e3a52606beff)



