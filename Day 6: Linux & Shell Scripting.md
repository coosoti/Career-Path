## DevOps Zero to Hero: Day 6 - Structured Notes

**Introduction:**

* This session introduces the Linux operating system and the fundamentals of shell scripting, crucial skills for DevOps engineers.
* The session aims to:
    * Explain the role of an operating system as an intermediary between hardware and software.
    * Highlight the reasons for Linux's popularity in production environments.
    * Provide a simplified overview of the Linux operating system architecture.
    * Introduce basic shell commands for file manipulation, directory navigation, and system monitoring.
    * Point the user to existing resources for deeper learning about shell scripting.

**Subtopics:**

1.  **Operating Systems (OS):**
    * An OS acts as a bridge between hardware (CPU, RAM, I/O) and software applications.
    * It manages hardware resources and facilitates communication between software and hardware.
    * Examples: Windows, macOS, Linux.
    * The OS is the core of a server or personal computer.

2.  **Why Linux is Popular:**
    * **Free and Open Source:**
        * Linux is freely available, reducing costs.
        * Open-source nature allows for customization and community support.
    * **Security:**
        * Linux is inherently more secure than Windows, often requiring less reliance on antivirus software.
    * **Variety of Distributions:**
        * Distributions like Ubuntu, CentOS, Debian, and Red Hat provide flexibility.
    * **Performance:**
        * Linux is known for its speed and stability, making it ideal for production servers.

3.  **Linux Operating System Architecture (Simplified):**
    * **Kernel:**
        * The core of the OS, responsible for communication between hardware and software.
        * Manages device, memory, and process management, and handles system calls.
    * **System Libraries:**
        * Provide functions and routines for applications to interact with the kernel.
        * Example: Libc.
    * **Compilers, User Processes, and System Software:**
        * Compilers translate code into executable programs.
        * User processes are applications running on the system.
        * System software provides essential utilities and services.

4.  **Fundamentals of Shell Scripting:**
    * **Shell:**
        * A command-line interface (CLI) that allows users to interact with the OS.
        * Essential for managing servers without a graphical user interface (GUI).
        * Bash is a very common shell.
    * **Basic Shell Commands:**
        * **`pwd` (Present Working Directory):** Displays the current directory.
        * **`ls` (List):** Lists files and directories in the current directory.
        * **`cd` (Change Directory):** Navigates to a different directory.
        * **`ls -ltr`:** Lists files and directories with detailed information (permissions, owner, size, timestamp).
        * **`touch`:** Creates an empty file.
        * **`vi`:** Opens a text editor to create or edit files.
            * Press `i` to enter insert mode, `Esc` then `:wq` to save and exit.
        * **`cat`:** Displays the contents of a file.
        * **`mkdir`:** Creates a directory.
        * **`rm`:** Removes a file.
        * **`rm -r`:** Removes a directory.
        * **`free -m`:** Displays memory usage.
        * **`nproc`:** Displays the number of processors.

5.  **System Monitoring Commands:**
    * **`free`:** Displays memory usage.
    * **`nproc`:** Displays number of processors.

6.  **System Monitoring Commands (Detailed):**
    * **`df -h` (Disk Free - Human-readable):**
        * Displays disk space usage in a human-readable format.
        * Shows total size, used space, available space, and usage percentage for each mounted file system.
    * **`free -m` (Free Memory - Megabytes):**
        * Displays memory usage in megabytes.
        * Shows total, used, free, shared, buffers, and cached memory.
    * **`nproc` (Number of Processors):**
        * Displays the number of processing units available.
        * Useful for determining the CPU capacity of the system.
    * **`top`:**
        * Provides a dynamic, real-time view of system processes.
        * Displays CPU and memory usage, running processes, and other system statistics.
        * A comprehensive tool for monitoring system performance.

7.  **Review of Shell Commands:**
    * The session covered commands for:
        * File and directory manipulation (creating, removing, editing, listing).
        * Directory navigation.
        * Viewing file permissions.
        * System monitoring (disk space, memory, CPU).


**Key Points:**

* `top` is a powerful command for monitoring overall system performance.
* Individual commands like `df -h`, `free -m`, and `nproc` provide specific information about disk space, memory, and CPU usage.
* Practical application of shell commands is essential for DevOps tasks.


**Conclusion:**

* Linux is a powerful and widely used OS in DevOps due to its free, secure, and fast nature.
* Shell scripting is essential for interacting with Linux systems and automating tasks.
* Understanding basic shell commands is crucial for managing Linux servers.
* The provided resources will help to learn more about Shell Scripting.
