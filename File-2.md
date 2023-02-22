# After file-1.md
------------------------------------
## checks if the package is installed, and if not, outputs the hostname of the server:
```
#!/bin/bash

# Define the package name
package_name="nginx"

# Check if the package is installed
if dpkg -s "$package_name" &> /dev/null; then
  echo "Package $package_name is installed"
else
  echo "Package $package_name is not installed on $(hostname)"
fi
```
----------------------------------------------
### bash script that creates variables for a package name and a server name, and installs the package on the specified server:
```
#!/bin/bash

# Define the package name and server name
package_name="nginx"
server_name="devserver"

# Check if the server is the specified one
if [ "$(hostname)" == "$server_name" ]; then
  # Install the package
  apt-get update
  apt-get install -y "$package_name"
  # Check if the package was successfully installed
  if dpkg -s "$package_name" &> /dev/null; then
    echo "Package $package_name was successfully installed on $(hostname)"
  else
    echo "Failed to install package $package_name on $(hostname)"
  fi
else
  echo "This script can only be run on $server_name"
fi
```
------------------------------
### bash script that creates variables for a package name and a server name, and installs the package on the specified server only if it is not already installed:
```
#!/bin/bash

# Define the package name and server name
package_name="nginx"
server_name="devserver"

# Check if the server is the specified one
if [ "$(hostname)" == "$server_name" ]; then
  # Check if the package is installed
  if ! dpkg -s "$package_name" &> /dev/null; then
    # Install the package
    apt-get update
    apt-get install -y "$package_name"
    # Check if the package was successfully installed
    if dpkg -s "$package_name" &> /dev/null; then
      echo "Package $package_name was successfully installed on $(hostname)"
    else
      echo "Failed to install package $package_name on $(hostname)"
    fi
  else
    echo "Package $package_name is already installed on $(hostname)"
  fi
else
  echo "This script can only be run on $server_name"
fi
```
-------------------------------
## bash script that changes the port 80 to 90 in a file named file.txt:
```
#!/bin/bash

# Define the file name
file_name="file.txt"

# Check if the file exists
if [ -f "$file_name" ]; then
  # Replace 80 with 90 in the file
  sed -i 's/80/90/g' "$file_name"
  echo "The port 80 in $file_name has been changed to 90."
else
  echo "The file $file_name does not exist."
fi
```


