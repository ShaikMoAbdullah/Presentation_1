# Operating System commands
## Table of contents
1. ps
2. top
3. df
4. uname
5. free
6. lspci
7. kill
8.  References

<br />

## 1. ps command - Process status
ps command is used to list the currently running processes and their PIDs along with some other information depending on different options. 

* ps - This command will show the process for the current shell.
~~~
    $ ps
~~~

  * PID – the unique process ID.
  * TTY – terminal type that the user is logged into.
  * TIME – amount of CPU in minutes and seconds that the process has been running.
  * CMD – name of the command that launched the process.
### Let us see some examples 
1. View all running processes

~~~
    $ ps -e
~~~
2. View all processes associated with the terminal

~~~
    $ ps -T
~~~
3. Show all current running processes.

~~~
    $ ps -ax 
~~~
>-a flag stands for **all** processes and -x will display the processes which are not associated with the current tty 

4. To filter processes according to the user.

~~~
    $ ps -u shaik
~~~

5. Display processes in a selected list of columns.
~~~
    $ ps -e -o pid,uname,pcpu,pmem,comm
~~~
6. Renaming column labels
~~~
    $ ps -e -o pid=PID,uname=Username,pcpu=CPU_usage,pmem=%Mem,comm=Command
~~~
7. Using ps command with grep to search for a particular process.
~~~
    $ ps -aef | grep systemd
~~~

<br />

## 2. top
It opens a interactive command mode where the top half portion will contain the statistics of processes and resource usage, And Lower half contains a list of the currently running processes.
* PID: Shows task’s unique process id.

~~~
    $ top
~~~
>Note:
>* **PR**: Stands for priority of the task.
>* **SHR**: Represents the amount of shared memory used by a task.
>* **VIRT**: Total virtual memory used by the task.
>* **USER**: User name of owner of task.
>* **%CPU**: Represents the CPU usage.
>* **TIME+**: CPU Time, the same as ‘TIME’, but reflecting more granularity through hundredths of a second.
>* **SHR**: Represents the Shared Memory size (kb) used by a task.
>* **%MEM**: Shows the Memory usage of task.

1. Exit Top Command After Specific repetition: top command will automatically exit after 10 number of repetition.
~~~
    $ top -n 10
~~~
2. Display specific user processes.
~~~
    $ top -u shaik
~~~
3. Highlight Running Process in Top: Press ‘z‘ option in running top command will display running process in color which may help you to identified running process easily.

4. Shows Absolute Path of Processes: Press ‘c‘ option in running top command, it will display absolute path of running programs.

5. Kill running process: You can kill a process after finding PID of process by pressing ‘k‘ option in running top command without exiting from top window as shown below.

7. Sort by CPU Utilisation: Press (Shift+P) to sort processes as per CPU utilization.     

<br />

## 3. df - disk free
It is used to display information related to file systems about total space and available space.

**Options**
* -a, –all: It includes pseudo, duplicate and inaccessible file systems.
* -h, –human-readable: Print sizes in power of 1024
* -l, –local: Limit listing to local file systems
* -t, –type=TYPE: Limit listing to file systems of type TYPE
* -T, –print-type: Print file system type
1. If no file name is given, it displays the space available on all currently mounted file systems.
~~~
    $ df 
~~~
2. Now, if you specify particular file, then it will show mount information of that particular file.
~~~
    $ df presentation/
~~~
3. If you want to display all the file system, use -a option.
~~~
    $ df -a
~~~
4. Use -h option to display size in power of 1024.
~~~
    $ df -h /home/shaik
~~~
5. To get complete grand total, use –total option
~~~
    $ df --total
~~~
6. Use -T option to display file type
~~~
    $ df -T /home/shaik
~~~
7. Display specific file system types.
~~~
    $ df -t ext4
~~~
8. Exclude the specific file system types.
~~~
    $ df -x ext4
~~~

## 4. uname
It displays the information about the system.
1. It prints all the system information in the following order: 
~~~
    $ uname -a
~~~
>It prints out Kernel name, network node hostname, kernel release date, kernel version, machine hardware name, hardware platform, operating system.
2. It prints the kernel name.
~~~
    $ uname -s
~~~
3. It prints the hostname of the network node(current computer)
~~~
    $ uname -n
~~~
4. It prints the kernel release date.
~~~
    $ uname -r
~~~
5. It prints the version of the current kernel.
~~~
    $ uname -v
~~~
* It prints the machine hardware name.
~~~
    $ uname -m
~~~
* It prints the name of the operating system.
~~~
    $ uname -o
~~~

## 5. free command

It displays the total amount of free space available along with the amount of memory used and swap memory in the system.
1. When no option is used then free command produces the columnar output.
~~~
    $ free
~~~
Options:

* -b, --bytes : It displays the memory in bytes.
* -k, --kilo : It displays the amount of memory in kilobytes(default).
* -m, --mega : It displays the amount of memory in megabytes.
* -g, --giga : It displays the amount of memory in gigabytes.
* --tera : It displays the amount of memory in terabytes.
* -h, --human : It shows all output columns in  human readable format.
* -t, --total : It adds an additional line in the output showing the column totals.
* -V, --version : It displays version info and exit.
    
1. Displays the output in **bytes**
~~~
    $ free -b
~~~
2. Displays the output in **gigabytes**.
~~~
    $ free -g
~~~
3. Displays the output with an additional line for **total**.
~~~
    $ free -t
~~~

## 6. lspci

This command is used to list information about the PCI(Peripheral component interconnect) connected devices on your system.  
~~~
$ lspci
~~~
There are actually 5 fields displayed in this output per line:
>* SLOT: 00:00.0
>* Class: Host bridge
>* Vendor: Intel Corporation
>* Device: 440FX – 82441FX PMC
>* Revision: 02

1. Another way of printing the lspci information.
~~~
    $ lspci -m
~~~
2. To get more verbose information.
~~~
    $ lspci -vmm
~~~
3. Lookup a Specific Device. When you know the slot number in the domain:bus:slot.func format.
~~~
    $ lspci -s 03:00:0
~~~
4. lspci -k --> This will display the kernel drivers.
~~~
    $ lspci -k
~~~

## 7. kill 

This command is used to terminate processes manually by sending signals.
>Note: If the user doesn’t specify any signal which is to be sent along with kill command then default TERM signal(-15) is sent that terminates the process.

**Syntax**:
~~~
kill [OPTIONS] [PID]...
~~~

The most commonly used signals are:
* 1 (HUP) - Reload a process.
* 9 (KILL) - Kill a process.
* 15 (TERM) - Gracefully stop a process.

Signals can be specified in three different ways:
* Using number (e.g., -1 or -s 1)
* Using the “SIG” prefix (e.g., -SIGHUP or -s SIGHUP)
* Without the “SIG” prefix (e.g., -HUP or -s HUP)


To display a list of running processes use the command ps and this will show you running processes with their PID number. 
~~~
$ ps
~~~
1. To show how to use pid with the kill command.
~~~
    $ kill pid
~~~
2. The command will print the PIDs and the PPID's of all Firefox processes:
~~~
    $ ps -aef | grep firefox
~~~
~~~
    $ pidof firefox
~~~

* Once you know the processes numbers, you can kill all of them by sending the TERM signal.

~~~
    $ kill -9 PID
~~~
3. Instead of searching for PIDs and then killing the processes, you can combine the above commands into one.
~~~
    $ kill -9 $(PID)
~~~

# References
* https://www.journaldev.com/24613/linux-ps-command
* https://www.geeksforgeeks.org/top-command-in-linux-with-examples/
* https://www.tecmint.com/12-top-command-examples-in-linux/
* https://www.javatpoint.com/linux-df
* https://www.geeksforgeeks.org/uname-command-in-linux-with-examples/
* https://www.thegeekstuff.com/2014/04/lspci-examples/
* https://linuxize.com/post/kill-command-in-linux/
* https://www.geeksforgeeks.org/free-command-linux-examples/