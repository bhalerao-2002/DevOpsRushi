### 1. Node health check
### 2. Running processes check
### 3. AWS resources check
### 4. Git-Organization users check
### 5. Deploy Application on AWS
### 6. 




# 1.a Write a shell script to check health of node.


```bash
vi healthCheck.sh
```

```bash
chmod 777 healthCheck.sh
```

```bash
./healthCheck.sh
```

### Script for 1a

```
#!/bin/bash

# Function to check CPU usage
check_cpu() {
    cpu_usage=$(top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | awk '{print 100 - $1}')
    echo "CPU Usage: $cpu_usage%"
}

# Function to check memory usage
check_memory() {
    memory_usage=$(free -m | awk 'NR==2{printf "Memory Usage: %.2f%%", $3*100/$2 }')
    echo "$memory_usage"
}

# Function to check disk usage
check_disk() {
    disk_usage=$(df -h / | awk 'NR==2{printf "Disk Usage: %s", $5}')
    echo "$disk_usage"
}

# Main function to call other health check functions
main() {
    echo "Checking Node Health..."
    check_cpu
    check_memory
    check_disk
}

# Call the main function
main

```

<br />

# 1.b Write a shell script to check running processes on linux.


```bash
vi CheckRunningProcess.sh
```

```bash
chmod 777 CheckRunningProcess.sh
```

```bash
./CheckRunningProcess.sh
```

### Script for 1b

```
#!/bin/bash

# Get list of running processes
process_list=$(ps aux)

# Print header
echo "PID   USER       %CPU   %MEM   COMMAND"

# Iterate through each line of process list
while read -r line; do
    # Skip the header line
    if [[ $line == USER* ]]; then
        continue
    fi

    # Extract PID, USER, %CPU, %MEM, and COMMAND
    pid=$(echo "$line" | awk '{print $2}')
    user=$(echo "$line" | awk '{print $1}')
    cpu=$(echo "$line" | awk '{print $3}')
    mem=$(echo "$line" | awk '{print $4}')
    command=$(echo "$line" | awk '{$1=$2=$3=$4=""; print $0}')

    # Print process information
    printf "%-6s %-9s %-6s %-6s %s\n" "$pid" "$user" "$cpu" "$mem" "$command"
done <<< "$process_list"

```
<br />

# 2. 

<br />

# 3.a Upload your project file on github using git commands.

```bash
  git init
  git add .
  git commit -m "first commit"
  git branch -M main
  git remote add origin https://github.com/bhalerao-2002/he-p.git
  git push -u origin main
```

<br /> 

#3.b Upload your project file on github using git commands.

```bash
git init
```
make changes in files 

```bash
git add .
git commit -m "Add AWS usage report script"
```
Switch Branches (Optional):

```bash
git checkout main
```
Merge Changes:
Once you're done with the changes in the aws_usage_report branch and you want to incorporate them into the main branch, you need to merge the branches:
```bash
git merge aws_usage_report
```
Delete branch: 
```bash
git branch -d aws_usage_report
```
Push branch:
```bash
git push origin main
```

<br />


