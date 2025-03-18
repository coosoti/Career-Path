## DevOps Zero to Hero: Day 5 - Structured Notes

**Introduction:**

* This session focuses on practical methods for accessing and automating the creation of AWS EC2 instances.
* The session aims to:
    * Demonstrate how to connect to an EC2 instance via the AWS Management Console and SSH.
    * Explain how to automate EC2 instance creation using the AWS CLI, CloudFormation Templates, and boto3 (Python SDK).
    * Provide practical guidance on authenticating with AWS and utilizing AWS documentation.
    * Assign a task to practice automating EC2 instance creation.

**Subtopics:**

1.  **Connecting to EC2 Instances:**
    * **AWS Management Console:**
        * Navigate to the EC2 dashboard.
        * Select the running instance.
        * Click "Connect" and follow the on-screen instructions.
        * Establishes a web-based SSH session.
    * **SSH (Secure Shell):**
        * Requires a terminal (e.g., iTerm2 on macOS, PuTTY or MobaXterm on Windows).
        * Obtain the instance's public IP address.
        * Use the `ssh` command with the private key file (`.pem`) and username (e.g., `ubuntu`).
        * Example: `ssh -i path/to/your/key.pem ubuntu@your_public_ip`
        * Change the permissions of the private key file to ensure security using `chmod 600 path/to/your/key.pem`.
        * SSH is generally preferred for automation and long-term connections.

2.  **Automating EC2 Instance Creation:**
    * **AWS CLI (Command-Line Interface):**
        * Install the AWS CLI.
        * Configure AWS credentials using `aws configure` (access key ID, secret access key, region).
        * Use `aws ec2 run-instances` command with required parameters (image ID, instance type, key pair, security groups, etc.).
        * Refer to AWS CLI documentation for command details and examples.
    * **AWS CloudFormation Templates (CFT):**
        * Declarative templates define desired infrastructure.
        * Create or use a sample CFT (available in AWS documentation or GitHub repositories).
        * Upload the CFT to AWS CloudFormation service.
        * CloudFormation provisions the resources defined in the template.
        * CFT is a form of Infrastructure as Code (IaC).
    * **boto3 (Python SDK):**
        * Install boto3 using `pip install boto3`.
        * Use Python scripts to interact with AWS services.
        * boto3 leverages the AWS API for programmatic access.
        * Example: Use boto3 to create EC2 instances, list running instances, etc.
        * boto3 uses the same credentials configured with `aws configure`.

3.  **AWS Authentication:**
    * **Security Credentials:**
        * Access AWS IAM (Identity and Access Management) service.
        * Create access keys (access key ID and secret access key).
        * Store credentials securely.
    * **AWS Configuration:**
        * Use `aws configure` command to set up credentials and default region.
        * Credentials are stored in a configuration file used by AWS CLI and boto3.

4.  **AWS Documentation:**
    * **AWS CLI Documentation:**
        * Comprehensive guide to AWS CLI commands and usage.
        * Provides examples and explanations for each command.
        * Essential resource for automating AWS tasks.
    * **boto3 Documentation:**
        * Explains how to use boto3 to interact with AWS services.
        * Provides examples and API reference for each service.
        * Valuable for Python-based AWS automation.
    * **AWS CloudFormation Documentation:**
        * Details the structure and syntax of CloudFormation templates.
        * Provides examples and best practices for using CloudFormation.

5.  **Assignment:**
    * Install the AWS CLI.
    * Create AWS security credentials and configure the CLI.
    * Use AWS CLI commands to:
        * List S3 buckets (`aws s3 ls`).
        * Create an S3 bucket (`aws s3 mb`).
        * Create an EC2 instance (`aws ec2 run-instances`).
    * Explore AWS CLI documentation for more commands and examples.

**Conclusion:**

* Automating EC2 instance creation is essential for efficient DevOps practices.
* AWS provides various tools for automation, including CLI, CFT, and boto3.
* Understanding AWS authentication and documentation is crucial for effective automation.
* Practical exercises and hands-on experience are vital for mastering AWS automation.
* The next sessions will delve deeper into Infrastructure as Code (IaC) and other DevOps concepts.
