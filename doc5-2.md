**Bash Scripting Exercises**

### 1. Introduction to Bash Scripting
**Exercise:** Write a Bash script that prints "Welcome to Bash scripting!" when executed.

**Answer:**
```bash
#!/bin/bash
echo "Welcome to Bash scripting!"
```

### 2. Variables in Bash
**Exercise:** Create a script that stores your name in a variable and prints "Hello, [Your Name]!"

**Answer:**
```bash
#!/bin/bash
name="Alice"
echo "Hello, $name!"
```

### 3. Conditional Statements
**Exercise:** Write a script that asks the user for a number and checks if it's even or odd.

**Answer:**
```bash
#!/bin/bash
echo "Enter a number:"
read num
if (( num % 2 == 0 )); then
    echo "The number is even."
else
    echo "The number is odd."
fi
```

### 4. Loops in Bash
**Exercise:** Write a script that prints numbers from 1 to 10 using a for loop.

**Answer:**
```bash
#!/bin/bash
for i in {1..10}; do
    echo "Number: $i"
done
```

### 5. Functions in Bash
**Exercise:** Create a function that takes a name as an argument and prints "Hello, [Name]!" Call this function with different names.

**Answer:**
```bash
#!/bin/bash
say_hello() {
    echo "Hello, $1!"
}
say_hello "Alice"
say_hello "Bob"
```

### 6. Working with Files and Directories
**Exercise:** Write a script that checks if a file named "data.txt" exists. If it does, print "File exists"; otherwise, create it.

**Answer:**
```bash
#!/bin/bash
if [ -f "data.txt" ]; then
    echo "File exists"
else
    touch data.txt
    echo "File created"
fi
```

### 7. User Input and Arguments
**Exercise:** Write a script that asks the user for their favorite programming language and prints a response using their input.

**Answer:**
```bash
#!/bin/bash
echo "What is your favorite programming language?"
read lang
echo "Nice choice! $lang is great!"
```

### 8. Error Handling and Debugging
**Exercise:** Modify one of your previous scripts to include debugging with `set -x` and disable it after debugging is done.

**Answer:**
```bash
#!/bin/bash
set -x
echo "Debugging mode enabled"
set +x
echo "Debugging mode disabled"
```

### 9. Working with Arrays
**Exercise:** Create an array with three fruit names. Print each fruit name using a loop.

**Answer:**
```bash
#!/bin/bash
fruits=("Apple" "Banana" "Cherry")
for fruit in "${fruits[@]}"; do
    echo "$fruit"
done
```

### 10. Scheduling and Automation
**Exercise:** Set up a cron job to run a script every hour that logs the current date and time into a file named "log.txt".

**Answer:**
```bash
crontab -e
# Add the following line:
0 * * * * echo "$(date)" >> /path/to/log.txt
```

### Bonus Challenge
**Exercise:** Write a script that backs up all `.txt` files from the current directory into a `backup` directory, creating it if necessary.

**Answer:**
```bash
#!/bin/bash
mkdir -p backup
cp *.txt backup/
echo "Backup completed."
```
