**Advanced Shell Scripting Concepts**

**Introduction:**

**Subtopics:**

1.  **Review of Part A and Node Health Monitoring:**
    * Part 1 covered basic shell scripting, file manipulation, and commands like `df` (disk space), `free` (memory), `nproc` (CPU), and `top` (process information).
    * These commands are essential for DevOps engineers to analyze node health.
    * This tutorial aims to build a custom node health script.
2.  **Best Practices in Shell Scripting:**
    * **Metadata Information:**
        * Including author name, creation date, script purpose, and version.
        * Provides clarity about the script's function and maintenance.
        * Example:
            ```bash
            #!/bin/bash
            # Author: Charles
            # Date: 2025-03-01
            # Purpose: Outputs node health
            # Version: v1
            ```
    * **Debug Mode (`set -x`):**
        * Using `set -x` enables debug mode, printing each command and its output.
        * Facilitates debugging and understanding script execution flow.
        * Example:
            ```bash
            #!/bin/bash
            set -x
            df -h
            free -g
            nproc
            ```
    * **Error Handling (`set -e` and `set -o pipefail`):**
        * `set -e`: Exits the script immediately if a command fails.
        * `set -o pipefail`: Ensures that the script exits if any command within a pipeline fails.
        * These commands improve script reliability by preventing further execution after an error.
        * Example:
            ```bash
            #!/bin/bash
            set -e
            set -o pipefail
            command_that_might_fail
            echo "This line will not be executed if the above command fails"
            ```
3.  **Process Management:**
    * **Listing Processes (`ps -ef` or `ps -aux`):**
        * `ps` (process status) command displays running processes.
        * Options like `-ef` provide full process details.
        * Example:
            ```bash
            ps -ef
            ```
    * **Filtering Processes with `grep`:**
        * `grep` filters the output of a command based on a pattern.
        * Used to find specific processes.
        * Example:
            ```bash
            ps -ef | grep "Amazon"
            ```
    * **Extracting Information with `awk`:**
        * `awk` is a powerful text-processing tool for extracting specific columns or fields from output.
        * It can be used to retrieve process IDs (PIDs) or other specific data.
        * Example (extracting PIDs):
            ```bash
            ps -ef | grep "Amazon" | awk '{print $2}'
            ```
4.  **Piping (`|`):**
    * The pipe operator (`|`) sends the output of one command to the input of another command.
    * Enables chaining commands for complex operations.
    * Example:
        ```bash
        command1 | command2 | command3
        ```
    * **Interview Question:**
        * `date | echo "Today is"` does not work as expected because `date` sends its output to `STDOUT`, and `echo` does not read from `STDIN` in the same way that `grep` does. `echo` simply prints the string provided.
5.  **File Handling and Log Analysis:**
    * **`curl`:**
        * `curl` retrieves data from or sends data to a server using URLs.
        * Used to download files, access APIs, and retrieve log files from remote locations.
        * Example:
            ```bash
            curl https://example.com/logfile.txt
            ```
    * **`wget`:**
        * `wget` downloads files from the web.
        * Differs from `curl` by saving the retrieved content to a file by default.
        * Example:
            ```bash
            wget https://example.com/logfile.txt
            ```
    * **Difference between `curl` and `wget`:**
        * `curl` displays output, while `wget` saves to a file.
        * Choice depends on whether you need to process the output directly or save it.
6.  **File Searching (`find`):**
    * `find` locates files and directories based on specified criteria (name, type, etc.).
    * Example:
        ```bash
        find / -name "pam.d"
        ```
    * `sudo` is often necessary to search the entire file system due to permission restrictions.
    * `sudo su -` is used to switch to the root user.
    * `su` switches to another user, and `sudo` executes commands with elevated privileges.
7.  **Conditional Logic (`if-else`):**
    * Shell scripts support `if-else` statements for conditional execution.
    * Syntax:
        ```bash
        if [ condition ]; then
          # Actions if condition is true
        elif [ another_condition ]; then # Optional
          # Actions if another_condition is true
        else
          # Actions if no condition is true
        fi
        ```
    * Example:
        ```bash
        a=4
        b=10
        if [ "$a" -gt "$b" ]; then
          echo "a is greater than b"
        else
          echo "b is greater than a"
        fi
        ```
8.  **Loops (`for`):**
    * `for` loops iterate over a sequence of values.
    * Syntax:
        ```bash
        for variable in values; do
          # Actions to perform for each value
        done
        ```
    * Example:
        ```bash
        for i in 1 2 3 4 5; do
          echo "Number: $i"
        done
        ```
9.  **Signal Trapping (`trap`):**
    * Signals are notifications sent to a process to indicate an event (e.g., interrupt, termination).
    * `trap` intercepts signals and executes a specified command.
    * Used to handle interrupts (e.g., Ctrl+C) gracefully or perform cleanup actions.
    * Example:
        ```bash
        trap "echo 'Ctrl+C caught! Cleaning up...'; exit 1" INT
        echo "Press Ctrl+C to interrupt..."
        while true; do
          sleep 1
        done
        ```
    * Common signals include `SIGINT` (interrupt, Ctrl+C).
    * Trapping signals is useful in scenarios where you want to prevent a script from being interrupted or to perform actions before a script terminates.

**Conclusion:**

This advanced shell scripting tutorial covered essential concepts for DevOps engineers, including best practices, process management, file handling, conditional logic, loops, and signal trapping. Mastering these concepts enables the creation of robust and efficient scripts for automating tasks, monitoring systems, and managing applications in a DevOps environment. The tutorial emphasizes the importance of understanding the underlying principles and using the appropriate commands for specific tasks.

**Advanced Shell Scripting Concepts - Expanded**

**1. Review of Part 1 and Node Health Monitoring:**

* **Expanding on Node Health:**
    * In a real-world DevOps environment, node health monitoring is crucial for maintaining application uptime and performance.
    * Beyond basic CPU, memory, and disk usage, you might monitor network latency, disk I/O, and application-specific metrics.
    * Scripts can be integrated with monitoring tools (e.g., Prometheus, Nagios) to trigger alerts when thresholds are exceeded.
    * **Example of a more complete health check:**
        ```bash
        #!/bin/bash
        # Check CPU usage
        cpu_usage=$(top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1" | awk '{print 100 - $1}')
        echo "CPU Usage: $cpu_usage%"

        # Check memory usage
        mem_usage=$(free -m | awk 'NR==2{printf "%.2f", $3/$2 * 100.0}')
        echo "Memory Usage: $mem_usage%"

        # Check disk usage
        disk_usage=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')
        echo "Disk Usage: $disk_usage%"

        # Check network connectivity (ping example)
        if ping -c 1 google.com > /dev/null; then
            echo "Network: OK"
        else
            echo "Network: FAIL"
        fi

        # Add logic to check for critical thresholds and send alerts.
        ```
        * This script expands on the previous examples by adding network connectivity checks.
        * It also stores the results in variables that can be used later to make automated decisions.

**2. Best Practices in Shell Scripting:**

* **Metadata Information - Importance:**
    * In collaborative environments, metadata helps other team members understand the script's purpose and usage.
    * It also serves as documentation for future maintenance and updates.
* **Debug Mode (`set -x`) - Advanced Use:**
    * `set -x` is invaluable for debugging complex scripts with loops and conditional statements.
    * It can be temporarily enabled for specific sections of a script to isolate issues.
    * Example of only debugging a part of a script.
        ```bash
        #!/bin/bash
        echo "start of script"
        set -x
        for i in {1..3}; do
            echo $i
        done
        set +x
        echo "end of script"
        ```
        * The set +x command turns off the debuging.
* **Error Handling (`set -e` and `set -o pipefail`) - Real-World Scenarios:**
    * In production environments, error handling is critical to prevent cascading failures.
    * `set -e` and `set -o pipefail` ensure that scripts fail fast, allowing for prompt issue resolution.
    * Example of a script that will fail.
        ```bash
        #!/bin/bash
        set -e
        set -o pipefail
        ls not_a_real_file | grep test
        echo "This line should not print"
        ```

**3. Process Management:**

* **`ps` Command - Advanced Options:**
    * `ps aux` provides a more comprehensive view of processes, including CPU and memory usage.
    * `ps -o pid,user,%cpu,%mem,command` customizes the output to display specific columns.
* **`grep` Command - Regular Expressions:**
    * `grep` supports regular expressions for more complex pattern matching.
    * Example: `ps aux | grep "[p]ython"` (finds Python processes without matching the grep command itself).
* **`awk` Command - Advanced Usage:**
    * `awk` can perform arithmetic operations, string manipulation, and conditional logic.
    * Example: `ps aux | awk '$3 > 50 {print $1, $11}'` (finds processes with CPU usage above 50%).
    * Awk is a programming language in and of itself.

**4. Piping (`|`) - Complex Pipelines:**

* Pipelines can be used to perform complex data transformations and filtering.
* Example of a complex pipe.
    ```bash
    cat /var/log/syslog | grep "error" | awk '{print $4,$5}' | sort | uniq -c | sort -nr
    ```
    * This pipeline gets errors from syslog, prints the time stamp of the error, sorts the errors, counts the unique errors, and then sorts them by the number of times they occure.
* **Redirecting Standard Error:**
    * `command 2>/dev/null` redirects standard error to `/dev/null`, suppressing error messages.
    * `command 2>&1` redirects standard error to standard output.

**5. File Handling and Log Analysis:**

* **`curl` Command - HTTP Methods:**
    * `curl -X POST -d '{"key": "value"}' https://api.example.com` sends a POST request with JSON data.
    * Curl can also be used to download files with progress bars.
    * `curl -O URL` will download the file, and keep the files original name.
* **`wget` Command - Recursive Downloads:**
    * `wget -r https://example.com` recursively downloads an entire website.
    * Wget is very useful for downloading large files.
* **Log Rotation and Analysis:**
    * Shell scripts can automate log rotation (archiving old logs) and analysis (searching for patterns).

**6. File Searching (`find`) - Advanced Options:**

* **`find` Command - File Types and Sizes:**
    * `find / -type f` finds all files.
    * `find / -size +1G` finds all files larger than 1 gigabyte.
    * `find / -mtime -7` finds all files modified in the last 7 days.
* **`find` Command - Executing Commands:**
    * `find / -name "*.txt" -exec rm {} \;` finds all text files and deletes them.
    * The {} is replaced with the file name.

**7. Conditional Logic (`if-else`) - Complex Conditions:**

* Shell scripts support logical operators (`-a` for AND, `-o` for OR) for complex conditions.
* Example of complex if statement.
    ```bash
    if [ "$cpu_usage" -gt 90 -a "$mem_usage" -gt 80 ]; then
        echo "Critial system load"
    fi
    ```
* The `case` statement is a more compact alternative to nested `if-else` statements.

**8. Loops (`for`) - Iterating Over Files and Directories:**

* `for file in *.txt; do ... done` iterates over all text files in the current directory.
* Example of a for loop that iterates over all files in a directory.
    ```bash
    for file in /var/log/*; do
        if [[ -f "$file" ]]; then
            echo "$file"
        fi
    done
    ```

**9. Signal Trapping (`trap`) - Handling Errors and Cleanup:**

* `trap` can be used to perform cleanup actions when a script is interrupted (e.g., deleting temporary files).
* Example of a trap that deletes temp files.
    ```bash
    #!/bin/bash
    temp_file=$(mktemp)
    trap "rm -f '$temp_file'" EXIT
    echo "creating temp file" > "$temp_file"
    sleep 10
    ```
    * In the above example, if the script is terminated, the temp file will be deleted.
* Trapping signals can prevent unintended data loss or corruption.

By expanding on these concepts with practical examples and real-world scenarios, you gain a deeper understanding of advanced shell scripting and its applications in DevOps.
