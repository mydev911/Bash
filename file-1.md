## bash script that reads a file line by line:
```
#!/bin/bash

filename="file.txt"

while read line; do
  echo "$line"
done < "$filename"
```
----------------------------
## bash script that checks if the line "i love you" exists in a file named file.txt

```
#!/bin/bash

filename="file.txt"

while read line; do
  if [ "$line" == "i love you" ]; then
    echo "Line found: $line"
    exit 0
  fi
done < "$filename"

echo "Line not found: i love you"
exit 1
```
-----------------
## bash script that counts the number of lines in a file named file.txt:
```
#!/bin/bash

filename="file.txt"

line_count=0
while read line; do
  ((line_count++))
done < "$filename"

echo "Number of lines: $line_count"
```
-----------------------------------
##  bash script that displays the last two lines of a file named file.txt:
```
#!/bin/bash

filename="file.txt"

lines=()
while read line; do
  lines+=("$line")
done < "$filename"

echo "Last two lines:"
echo "${lines[-2]}"
echo "${lines[-1]}"
```
-----------------------
## bash script that displays the first two lines of a file named file.txt:
```
 #!/bin/bash

filename="file.txt"

count=0
while read line && [ $count -lt 2 ]; do
  echo "$line"
  ((count++))
done < "$filename"
```
-------------------------
## bash script that displays the changes made to a file named file.txt in the last one day
```
#!/bin/bash

filename="file.txt"

# Get the modification time of the file
modification_time=$(stat -c %Y "$filename")

# Get the current time
current_time=$(date +%s)

# Calculate the difference in seconds between the current time and modification time
difference=$((current_time - modification_time))

# If the difference is less than 86400 seconds (1 day), display the changes
if [ $difference -lt 86400 ]; then
  echo "Changes in the last one day:"
  echo ""
  # Use the 'tail' command to display the last few lines of the file
  tail "$filename"
else
  echo "No changes in the last one day."
fi
```
------------------------------------
## bash script to check package nginx is installed or not on multiple servers
```
#!/bin/bash

# Define the list of servers
servers=(server1 server2 server3)

# Loop through the list of servers
for server in "${servers[@]}"; do
  # For a Debian-based system (such as Ubuntu)
  if ssh $server "dpkg -s nginx 2>/dev/null | grep -q '^Status.*installed'" ; then
    echo "nginx is installed on $server"
  else
    echo "nginx is not installed on $server"
  fi

  # For a Red Hat-based system (such as Fedora or CentOS)
  if ssh $server "rpm -qa | grep -q nginx" ; then
    echo "nginx is installed on $server"
  else
    echo "nginx is not installed on $server"
  fi
done
```
-----------------------
## ash script that creates a variable for the package name, checks if the package is installed, and installs it if it's not installed:
```
#!/bin/bash

# Define the package name
package="nginx"

# Define the list of servers
servers=(server1 server2 server3)

# Loop through the list of servers
for server in "${servers[@]}"; do
  # For a Debian-based system (such as Ubuntu)
  if ssh $server "dpkg -s $package 2>/dev/null | grep -q '^Status.*installed'" ; then
    echo "$package is already installed on $server"
  else
    echo "$package is not installed on $server, installing it now..."
    ssh $server "sudo apt-get update && sudo apt-get install -y $package"
  fi

  # For a Red Hat-based system (such as Fedora or CentOS)
  if ssh $server "rpm -qa | grep -q $package" ; then
    echo "$package is already installed on $server"
  else
    echo "$package is not installed on $server, installing it now..."
    ssh $server "sudo yum update && sudo yum install -y $package"
  fi
done
```
---------------------------------------
## bash script that creates a variable for the source and destination paths, and copies a file from the source to the destination:
```
#!/bin/bash

# Define the source and destination paths
src_path="/path/to/source/file.txt"
dst_path="/path/to/destination/file.txt"

# Check if the source file exists
if [ -f "$src_path" ]; then
  # Copy the file from the source to the destination
  cp "$src_path" "$dst_path"
  # Check if the file was successfully copied
  if [ $? -eq 0 ]; then
    echo "File successfully copied from $src_path to $dst_path"
  else
    echo "Failed to copy file from $src_path to $dst_path"
  fi
else
  echo "Source file $src_path does not exist"
fi
```
-----------------------------------------------------
## bash script that creates a variable for a file path and checks if the file exists:
```
#!/bin/bash

# Define the file path
file_path="/path/to/file.txt"

# Check if the file exists
if [ -f "$file_path" ]; then
  echo "File $file_path exists"
else
  echo "File $file_path does not exist"
fi
```
# Follow Next File-2.md
