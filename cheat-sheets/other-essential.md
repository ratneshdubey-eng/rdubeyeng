# Essential Terminal Commands Cheat Sheet

### Overview
This cheat sheet provides a comprehensive list of frequently used macOS terminal commands tailored for developers. It includes commands for file management, process management, Git version control, networking, system monitoring, and more. Designed to improve productivity, these commands are organized into categories to facilitate quick reference.

### Table of Contents
1. [File & Directory Management](#1-file--directory-management)
2. [File Permissions & Ownership](#2-file-permissions--ownership)
3. [Searching & Finding Files](#3-searching--finding-files)
4. [System Information & Resource Monitoring](#4-system-information--resource-monitoring)
5. [Networking Commands](#5-networking-commands)
6. [Package Management (Homebrew)](#6-package-management-homebrew)
7. [Git Commands for Version Control](#7-git-commands-for-version-control)
8. [File Compression & Archiving](#8-file-compression--archiving)
9. [Process Management](#9-process-management)
10. [System Updates & Upgrades](#10-system-updates--upgrades)

---

### 1. **File & Directory Management**
| Command                                      | Description                                         |
|----------------------------------------------|-----------------------------------------------------|
| `ls`                                         | List directory contents.                            |
| `ls -la`                                      | List all files (including hidden) with detailed info.|
| `cd <directory>`                             | Change directory.                                   |
| `cd ..`                                       | Move up one directory level.                        |
| `pwd`                                        | Show the current directory path.                    |
| `mkdir <directory>`                          | Create a new directory.                             |
| `rmdir <directory>`                          | Remove an empty directory.                          |
| `rm <file>`                                  | Delete a file.                                      |
| `rm -r <directory>`                          | Recursively delete a directory and its contents.    |
| `mv <source> <destination>`                  | Move/rename a file or directory.                    |
| `cp <source> <destination>`                  | Copy a file or directory.                           |
| `touch <file>`                               | Create an empty file or update a file's timestamp.  |

### 2. **File Permissions & Ownership**
| Command                                      | Description                                         |
|----------------------------------------------|-----------------------------------------------------|
| `chmod <permissions> <file>`                 | Change file permissions (e.g., `chmod 755 script.sh`).|
| `chown <user>:<group> <file>`                | Change file owner and group.                        |
| `sudo`                                       | Execute a command as the superuser.                 |

### 3. **Searching & Finding Files**
| Command                                      | Description                                         |
|----------------------------------------------|-----------------------------------------------------|
| `find <directory> -name "<filename>"`         | Find files by name in a directory.                  |
| `grep "<pattern>" <file>`                    | Search for a pattern in a file.                     |
| `grep -r "<pattern>" <directory>`            | Recursively search for a pattern in a directory.    |
| `locate <filename>`                          | Find the location of a file.                        |

### 4. **System Information & Resource Monitoring**
| Command                                      | Description                                         |
|----------------------------------------------|-----------------------------------------------------|
| `top`                                        | Display running processes.                          |
| `htop`                                       | An enhanced version of `top` (requires installation).|
| `ps -ax`                                     | Show all running processes.                         |
| `df -h`                                      | Display free disk space.                            |
| `du -sh <directory>`                         | Show the size of a directory.                       |
| `free -h`                                    | Show free and used memory.                          |
| `system_profiler SPHardwareDataType`         | View detailed system hardware information.          |

### 5. **Networking Commands**
| Command                                      | Description                                         |
|----------------------------------------------|-----------------------------------------------------|
| `ifconfig`                                   | Display network configuration.                      |
| `ping <host>`                                | Test connectivity to a host.                        |
| `curl <url>`                                 | Make HTTP requests (e.g., `curl -I <url>` for headers).|
| `wget <url>`                                 | Download files from a URL (requires installation).  |
| `telnet <host> <port>`                       | Connect to a remote host on a specific port.        |
| `ssh <user>@<host>`                          | Securely connect to a remote machine.               |

### 6. **Package Management (Homebrew)**
| Command                                      | Description                                         |
|----------------------------------------------|-----------------------------------------------------|
| `brew install <package>`                     | Install a package using Homebrew.                   |
| `brew uninstall <package>`                   | Remove a package installed via Homebrew.            |
| `brew update`                                | Update Homebrew and its packages.                   |
| `brew upgrade <package>`                     | Upgrade a specific package to the latest version.   |
| `brew services start <service>`              | Start a background service (e.g., `brew services start mysql`). |
| `brew list`                                  | List all installed packages.                        |

### 7. **Git Commands for Version Control**
| Command                                      | Description                                         |
|----------------------------------------------|-----------------------------------------------------|
| `git status`                                 | Show the status of the working directory.           |
| `git add <file>`                             | Stage a file for commit.                            |
| `git commit -m "<message>"`                   | Commit staged changes with a message.               |
| `git push <remote> <branch>`                 | Push changes to the remote repository.              |
| `git pull <remote> <branch>`                 | Pull updates from the remote repository.            |
| `git checkout <branch>`                      | Switch to a different branch.                       |
| `git branch -d <branch>`                     | Delete a local branch.                              |
| `git clone <repository-url>`                 | Clone a repository from a URL.                      |
| `git log --oneline`                          | Show a condensed history of commits.                |

### 8. **File Compression & Archiving**
| Command                                      | Description                                         |
|----------------------------------------------|-----------------------------------------------------|
| `tar -cvf <archive-name>.tar <directory>`    | Create a tar archive.                               |
| `tar -xvf <archive-name>.tar`                | Extract a tar archive.                              |
| `zip <archive-name>.zip <file/directory>`    | Create a zip archive.                               |
| `unzip <archive-name>.zip`                   | Extract a zip archive.                              |

### 9. **Process Management**
| Command                                      | Description                                         |
|----------------------------------------------|-----------------------------------------------------|
| `ps`                                         | Display currently running processes.                |
| `kill <PID>`                                 | Terminate a process by its PID.                     |
| `kill -9 <PID>`                              | Forcefully terminate a process.                     |
| `pkill <process-name>`                       | Kill a process by name.                             |
| `bg`                                         | Resume a suspended job in the background.           |
| `fg`                                         | Bring a job to the foreground.                      |

### 10. **System Updates & Upgrades**
| Command                                      | Description                                         |
|----------------------------------------------|-----------------------------------------------------|
| `softwareupdate --list`                      | List all available macOS updates.                   |
| `softwareupdate --install --all`             | Install all available updates.                      |
| `brew upgrade`                               | Upgrade all Homebrew packages.                      |
| `brew cleanup`                               | Remove old versions of installed packages.          |

