**Shell Scripting Interview Questions**

**Introduction:**

This document focuses on common shell scripting interview questions, emphasizing practical knowledge and day-to-day usage. The goal is to prepare for technical interviews by covering frequently asked questions and providing detailed explanations.

**Subtopics:**

1.  **Commonly Used Shell Commands:**
    * Interviewers assess practical experience by asking about frequently used commands.
    * Emphasis on honesty and relevance to daily tasks.
    * Examples of common commands:
        * `ls`: List files and directories.
        * `cp`: Copy files.
        * `mv`: Move files.
        * `mkdir`: Create directories.
        * `touch`: Create files.
        * `vim`: Open files for editing.
        * `grep`: Filter output.
        * `find`: Locate files.
        * `top`, `sar`: System monitoring.
        * `df`: Check disk space.
    * Avoid mentioning niche commands (e.g., `netcat`, `traceroute`) unless specifically relevant, as they are typically used for debugging rather than routine tasks.

2.  **Listing Processes:**
    * `ps -ef` lists all running processes with detailed information.
    * To extract process IDs (PIDs):
        * Use `awk` to filter output: `ps -ef | awk '{print $2}'`.
        * `awk` is used to print the second column, which contains the PIDs.

3.  **Filtering Remote Logs:**
    * Use `curl` to retrieve remote log files (e.g., from Google Storage, S3).
    * Combine `curl` with `grep` to filter specific log entries (e.g., error messages).
    * Example: `curl <log_file_url> | grep "error"`.
    * The pipe (`|`) operator sends the output of `curl` to `grep`.
    * Example with a provided URL: `curl <URL_to_log_file> | grep "Trace"`
    * This demonstrates how to get trace log entries.

4.  **Conditional Printing of Numbers:**
    * Task: Print numbers divisible by 3 and 5, but not by 15, within a given range (e.g., 1-100).
    * Break down the problem:
        * Divisible by 3.
        * Divisible by 5.
        * Not divisible by 15.
    * Use a `for` loop to iterate through the range.
    * Use `if` statements with modulo operator (`%`) to check divisibility.
    * Example Script:
        ```bash
        #!/bin/bash
        for i in {1..100}; do
          if [[ $((i % 3)) -eq 0 || $((i % 5)) -eq 0 ]] && [[ $((i % 15)) -ne 0 ]]; then
            echo $i
          fi
        done
        ```
    * Explanation:
        * `$((i % 3)) -eq 0`: Checks if `i` is divisible by 3.
        * `$((i % 5)) -eq 0`: Checks if `i` is divisible by 5.
        * `$((i % 15)) -ne 0`: Checks if `i` is not divisible by 15.
        * `||` is a logical OR, and `&&` is a logical AND.

5.  **Counting Character Occurrences:**
    * Task: Count the number of occurrences of a specific character (e.g., 's') in a string (e.g., "Mississippi").
    * Use `grep -o` to extract each occurrence of the character on a new line.
    * Use `wc -l` to count the number of lines (occurrences).
    * Example:
        ```bash
        #!/bin/bash
        string="Mississippi"
        count=$(echo $string | grep -o "s" | wc -l)
        echo $count
        ```
    * `-o` with `grep`, means only print the matching part of the line.
    * `wc -l` means word count, and only print the number of lines.

6.  **Debugging Shell Scripts:**
    * Use `set -x` at the beginning of the script to enable debug mode.
    * This prints each command and its arguments as they are executed.

7.  **Cron Tab:**
    * Cron tab is a time-based job scheduler in Linux.
    * It allows automating tasks to run at specific times or intervals.
    * Example use case: Scheduling a daily report generation script.

8.  **Opening Files in Read-Only Mode:**
    * Use `vim -R <filename>` to open a file in read-only mode with the `vim` editor.

9.  **Soft Links vs. Hard Links:**
    * **Hard Links:**
        * Create a direct copy or mirror of a file.
        * Even if the original file is deleted, the hard link remains.
        * Multiple hard links share the same inode.
    * **Soft Links (Symbolic Links):**
        * Create a shortcut or alias to a file.
        * If the original file is deleted, the soft link becomes broken.
        * Used for creating aliases (e.g., `python` pointing to `python3`).

10. **Break and Continue Statements:**
    * **Break:**
        * Exits the loop prematurely.
        * Used to terminate a loop when a specific condition is met.
    * **Continue:**
        * Skips the current iteration of the loop.
        * Continues with the next iteration.

11. **Disadvantages of Shell Scripting:**
    * Dynamically typed: Lack of static type checking can lead to runtime errors.
    * Error handling can be less robust than in compiled languages.
    * Performance limitations for complex tasks.
    * Lack of complex data structures.

12. **Types of Loops:**
    * `for` loop: Iterates over a sequence of values.
    * `while` loop: Executes a block of code as long as a condition is true.
    * `until` loop: Executes a block of code until a condition is true.
    * Understanding when to use each loop type is essential.

13. **Dynamic vs. Static Typing:**
    * **Dynamically Typed (e.g., Shell, Python):**
        * Variable types are checked at runtime.
        * Flexibility but potential for runtime errors.
    * **Statically Typed (e.g., Go, Java):**
        * Variable types are checked at compile time.
        * Improved type safety and early error detection.

14. **Network Troubleshooting Tools:**
    * `traceroute`: Traces the route packets take to reach a destination, identifying network hops and latency.
    * `tracepath`: Similar to traceroute but does not require root privileges.

15. **Sorting Lists:**
    * Use the `sort` command to sort lines in a file or input.
    * Linux natively has this command.

16. **Log Management:**
    * Use `logrotate` to manage log files, preventing disk space exhaustion.
    * `logrotate` can compress, rotate, and delete old log files based on defined policies.
    * Example: Rotate logs daily, compress them, and keep them for 30 days.

**Conclusion:**

This document provides a comprehensive overview of common shell scripting interview questions. It emphasizes practical knowledge, efficient command usage, and problem-solving skills. By understanding these concepts and practicing the examples, one can enhance their readiness for technical interviews and improve their proficiency in shell scripting.
