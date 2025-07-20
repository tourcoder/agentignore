# .agentignore
A Control Mechanism for AI Agent

[ENGLISH VERSION](/README.md), [简体中文版](/README-zhcn.md)

### 1. Introduction for Users

Welcome! This document introduces `.agentignore`, a simple yet powerful way designed to give you precise control over which parts of your codebase AI agents and code assistants can access.

As AI becomes an integral part of our development workflow, it's crucial to ensure that sensitive information, experimental code, or irrelevant files are not processed or exposed. The `.agentignore` file works just like the familiar `.gitignore` file, but it's specifically for AI tools. By creating an `.agentignore` file in your project's root directory, you can list files and directories that you want AI agents to completely ignore.

This helps you:

* **Protect Sensitive Data**: Prevent AI from accessing files containing API keys, credentials, or personal information.
* **Reduce Noise**: Exclude logs, build artifacts, and dependency folders (like `node_modules`) to help the AI focus on relevant source code.
* **Improve Performance**: By ignoring unnecessary files, AI tools can process your requests faster and provide more accurate results.

### 2. Specification for Users: How to Use `.agentignore`

Creating and using an `.agentignore` file is straightforward.

1.  **Create the File**: In the root directory of your project, create a new file named `.agentignore`.
2.  **Add Rules**: Open the file and add patterns for files and directories you wish to exclude. The syntax is identical to `.gitignore`.

#### Syntax Rules:

* **Blank Lines**: Empty lines are ignored and can be used for spacing.
* **Comments**: Lines starting with `#` are treated as comments and are ignored.
* **Files**: Simply write the name of the file (e.g., `credentials.json`).
* **Directories**: To ignore an entire directory, add its name followed by a slash `/` (e.g., `node_modules/`).
* **Wildcards**: Use asterisks `*` as a wildcard. For example, `*.log` will ignore all files ending with `.log`.
* **Negation**: To make an exception to a rule, prefix it with an exclamation mark `!` 

#### Example `.agentignore` file:

**Ignore dependency directories**

node_modules/  
vendor/

**Ignore build output**

dist/  
build/  
*.o  
*.out

**Ignore sensitive configuration files**

.env  
config/secrets.yml  
api-keys.txt

**Ignore logs and temporary files**

*.log  
*.tmp  
temp/

**Ignore system-specific files**

.DS_Store  
Thumbs.db

By placing this file in your project, any compliant AI tool will know to skip these specified paths during its operations.

### 3. Implementation Guide for IDE & AI Agent Developers

To integrate support for `.agentignore` into your IDE extension or AI agent, you need to implement a file discovery and parsing mechanism. The goal is to respect the user's intent to exclude certain files and directories from AI processing.

#### Core Logic:

1.  **File Discovery**: When an AI agent is activated on a file or directory, it must look for an `.agentignore` file. The search should start in the directory of the current file and traverse upwards to the project root. The rules from all found `.agentignore` files should be combined (though typically, one in the root is sufficient).

2.  **Parsing**: The parser should read the `.agentignore` file line by line.
    * Trim whitespace from each line.
    * Ignore lines that are empty or start with `#`.
    * Each remaining line is a pattern.

3.  **Path Matching Algorithm**: Before accessing any file or directory, the agent must check its path against the collected patterns.
    * The path should be relative to the location of the `.agentignore` file.
    * If the path matches any pattern in the `.agentignore` file, the agent **MUST NOT** read, process, or include the file/directory in its context.
    * The matching logic should support standard glob patterns (`*`, `**`, `?`). For consistency, it is highly recommended to use a library that replicates the behavior of `.gitignore` matching.

### 4. Contributing: How to Submit a Pull Request (PR)

We welcome contributions to improve `.agentignore`! Here are the steps to contribute:

1. **Fork the Repository**: Start by forking this repository to your GitHub account.
2. **Create a New Branch**: Create a new branch for your changes. For example, `feature/add-ignore-pattern`.
3. **Make Your Changes**: Implement the desired changes in your branch. Make sure to follow the project's coding style and guidelines.
4. **Test Your Changes**: Ensure your changes work as expected and do not break any existing functionality.
5. **Submit a Pull Request**: Once your changes are ready, submit a pull request (PR) to the main repository. In your PR description, clearly explain the changes you've made and why they are needed.
6. **Address Feedback**: If the project maintainers have feedback or request changes, be sure to address them and update your PR.

Please ensure your contributions follow these guidelines to maintain consistency and quality across the project.

Thank you for contributing!

### 5. Acknowledgements

This project would not have been possible without the open-source contributions of countless individuals. Special thanks to the creators of [gitignore](https://github.com/github/gitignore) for their foundational work on ignore file patterns.

### 6. License

This project is licensed under the [Apache 2.0 License](/LICENSE).
