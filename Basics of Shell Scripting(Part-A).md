Certainly! Let's expand on the structured notes with practical shell script examples for each of the major subtopics.

**DevOps Zero to Hero: Shell Scripting Fundamentals - Expanded with Scripts**

**Introduction:**

Absolutely! I've reviewed the three parts of the transcript you provided and have compiled them into structured notes, following your guidelines.

**DevOps Zero to Hero: Shell Scripting Fundamentals**

**Introduction:**

This tutorial introduces the fundamentals of shell scripting within the context of DevOps. It explains the importance of automation in Linux environments, particularly for DevOps engineers, and covers essential shell commands for file manipulation, system monitoring, and task automation. The tutorial also addresses the purpose of the shebang (`#!/bin/bash`), file permissions using `chmod`, and the practical application of shell scripting in real-world DevOps scenarios.

**Subtopics:**

1.  **Automation and Shell Scripting:**
    * Automation reduces manual effort in repetitive tasks.
    * Shell scripting automates tasks on Linux-based systems, including those hosted on cloud platforms like AWS.
    * Examples of automatable tasks include file creation, system monitoring, and configuration management.
2.  **Basic Shell Commands:**
    * **File and Directory Manipulation:**
        * `touch`: Creates empty files.
        * `vim`/`vi`: Opens a text editor for creating and editing files. Vim is an improved version of vi.
        * `cat`: Displays file contents.
        * `ls`: Lists files and directories.
        * `mkdir`: Creates directories.
        * `rm`: Removes files.
        * `rm -r`: Removes directories.
    * **Navigation and Information:**
        * `cd`: Changes directories.
        * `pwd`: Displays the present working directory.
        * `man`: Displays the manual page for a command.
        * `history`: Displays a history of previously executed commands.
    * **Permissions:**
        * `chmod`: Changes file permissions.
        * Permissions are granted to the owner, group, and others.
        * The 4-2-1 principle (read, write, execute) is used to set permissions numerically.
3.  **Shebang (`#!/bin/bash`) and Shell Selection:**
    * The shebang specifies the interpreter for the script.
    * `#!/bin/bash` is used for Bash scripts.
    * The choice of shell (Bash, sh, Dash, ksh) affects script behavior due to syntax differences.
    * Historically, `#!/bin/sh` often linked to Bash, but now it may link to Dash on some systems, leading to potential compatibility issues.
4.  **File Permissions (`chmod`):**
    * Linux requires explicit permissions to execute files for security.
    * `chmod` grants permissions using numerical or symbolic modes.
    * The numerical mode uses the 4-2-1 principle (read, write, execute) to represent permissions for the owner, group, and others.
    * `chmod 777 filename.sh` grants full permissions to everyone.
5.  **System Monitoring Commands:**
    * `nproc`: Displays the number of processors.
    * `free`: Displays memory usage.
    * `top`: Provides a real-time view of system processes, CPU, and memory usage.
6.  **DevOps Applications of Shell Scripting:**
    * Automating infrastructure maintenance.
    * Managing code with Git repositories.
    * Configuration management.
    * Monitoring system health (CPU, RAM) and sending notifications.
    * Example: A script to monitor the health of 10,000 virtual machines and send alerts.
7.  **Advanced Shell Scripting (Brief Overview):**
    * Signal trapping (`trap`): Handling interrupts and signals.
    * Cron jobs: Scheduling tasks to run automatically.

**Conclusion:**

Shell scripting is a fundamental skill for DevOps engineers, enabling automation and efficient management of Linux systems. This tutorial provided a solid foundation in basic shell commands, file permissions, and system monitoring, along with practical examples of how these skills are applied in real-world DevOps scenarios. Further exploration of advanced topics like signal trapping and cron jobs can enhance automation capabilities.

**Subtopics:**

1.  **Automation and Shell Scripting:**
    * **Example: Automating File Creation**
        ```bash
        #!/bin/bash
        # Create 10 empty files
        for i in {1..10}; do
          touch "file_$i.txt"
          echo "Created file_$i.txt"
        done
        ```
        * This script uses a `for` loop to create 10 files named `file_1.txt` through `file_10.txt`.

2.  **Basic Shell Commands:**
    * **File and Directory Manipulation:**
        * **Example: Creating and Editing a File**
            ```bash
            #!/bin/bash
            touch my_script.sh
            echo "echo 'Hello, World!'" > my_script.sh
            chmod +x my_script.sh #Make it executable
            ./my_script.sh
            ```
            * Creates `my_script.sh`, writes an `echo` command into it, makes it executable, and then executes it.
        * **Example: Recursive Directory Removal**
            ```bash
            #!/bin/bash
            mkdir -p test_dir/subdir
            touch test_dir/file.txt
            touch test_dir/subdir/file2.txt
            rm -r test_dir
            echo "test_dir removed"
            ```
            * Creates a directory structure and then removes it recursively.
    * **Navigation and Information:**
        * **Example: Displaying Current Directory and Listing Files**
            ```bash
            #!/bin/bash
            echo "Current directory: $(pwd)"
            echo "Files in current directory:"
            ls -l
            ```
            * Displays the current directory and lists files with detailed information.
    * **Permissions:**
        * **Example: Changing File Permissions**
            ```bash
            #!/bin/bash
            touch permissions_test.txt
            chmod 644 permissions_test.txt #Owner read/write, group/others read
            ls -l permissions_test.txt
            chmod 755 permissions_test.txt #Owner read/write/execute, group/others read/execute
            ls -l permissions_test.txt
            ```
            * Changes permissions of a file and shows the effect with `ls -l`.

3.  **Shebang (`#!/bin/bash`) and Shell Selection:**
    * **Example: Demonstrating Bash Script Execution**
        ```bash
        #!/bin/bash
        echo "This script is executed using Bash."
        echo "Bash version: $BASH_VERSION"
        ```
        * Verifies that the script is running with Bash.
    * **Example of using `#!/bin/sh`**
        ```bash
        #!/bin/sh
        echo "This script is executed using sh."
        ```
        * This script will be executed with sh. On some systems this will be dash, and on others bash.

4.  **File Permissions (`chmod`):**
    * **Example: Using Numerical Permissions**
        ```bash
        #!/bin/bash
        touch my_executable.sh
        chmod 700 my_executable.sh # Owner: rwx, Group/Others: ---
        ls -l my_executable.sh
        ```
        * Grants execute permission only to the owner.

5.  **System Monitoring Commands:**
    * **Example: Displaying System Information**
        ```bash
        #!/bin/bash
        echo "Number of CPUs: $(nproc)"
        echo "Memory Usage:"
        free -m
        echo "Top Processes:"
        top -n 1 | head -n 15 #Display top 15 processes once.
        ```
        * Displays CPU count, memory usage, and the top processes.

6.  **DevOps Applications of Shell Scripting:**
    * **Example: Simple System Health Check (Conceptual)**
        ```bash
        #!/bin/bash
        # Simplified example - in real use case you would use SSH to remote machines.
        cpu_usage=$(top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1" | awk '{print 100 - $1}')
        mem_usage=$(free -m | awk 'NR==2{printf "%.2f", $3/$2 * 100.0}')

        echo "CPU Usage: $cpu_usage%"
        echo "Memory Usage: $mem_usage%"

        if [[ "$cpu_usage" -gt 90 ]]; then
            echo "Warning: High CPU usage!"
        fi

        if [[ "$mem_usage" -gt 80 ]]; then
            echo "Warning: High Memory usage!"
        fi
        ```
        * A basic script to check CPU and memory usage. A real world script would need to use ssh to connect to remote servers.

7.  **Advanced Shell Scripting (Brief Overview):**
    * **Example: Signal Trapping**
        ```bash
        #!/bin/bash
        trap "echo 'Ctrl+C caught! Cleaning up...'; exit 1" INT
        echo "Press Ctrl+C to interrupt..."
        while true; do
          sleep 1
        done
        ```
        * Traps the `INT` signal (Ctrl+C) and performs cleanup before exiting.
    * **Example: Cron Job (Conceptual)**
        * To schedule a script to run daily, add a line like this to your crontab (using `crontab -e`):
            ```cron
            0 0 * * * /path/to/my_script.sh
            ```
            * This runs `my_script.sh` every day at midnight.

These scripts provide a practical foundation for understanding the concepts covered in the notes. Remember to make the scripts executable using `chmod +x script_name.sh` before running them.

