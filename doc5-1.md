**Bash Scripting Basics**


**Example:**
```bash
#!/bin/bash
echo "Hello, World!"
```

### 1. Variables in Bash
- Defining and using variables

**Example:**
```bash
#!/bin/bash
name="Alice"
echo "Hello, $name"
```

### 2. Conditional Statements
- If-else statements

**Example:**
```bash
#!/bin/bash
num=10
if [ $num -gt 5 ]; then
    echo "The number is greater than 5"
else
    echo "The number is 5 or less"
fi
```

### 3. Loops in Bash
- For loops

**Example:**
```bash
#!/bin/bash
for i in {1..5}; do
    echo "Iteration: $i"
done
```

### 4. Functions in Bash
- Defining functions
- Calling functions

**Example:**
```bash
#!/bin/bash
say_hello() {
    echo "Hello, $1!"
}
say_hello "Alice"
```

### 5 Working with Files and Directories
- Creating and deleting files/directories
- Checking file existence

**Example:**
```bash
#!/bin/bash
if [ -f "file.txt" ]; then
    echo "file.txt exists"
else
    echo "file.txt does not exist"
fi
```

### 6. User Input and Arguments
- Reading user input
- Passing arguments to scripts

**Example:**
```bash
#!/bin/bash
echo "Enter your name:"
read name
echo "Hello, $name"
```

### 7. Error Handling and Debugging
- Debugging with `set -x`

**Example:**
```bash
#!/bin/bash
set -x
echo "Debugging mode enabled"
set +x
echo "Debugging mode disabled"
```

### 9. Working with Arrays
- Defining and accessing arrays

**Example:**
```bash
#!/bin/bash
fruits=("Apple" "Banana" "Cherry")
echo "First fruit: ${fruits[0]}"
```

### 9. Scheduling and Automation
- Using cron jobs
- Automating tasks

**Example:**
```bash
crontab -e
# Add the following line to run script.sh every day at midnight
0 0 * * * /path/to/script.sh
```


