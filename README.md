# Wrapper Tools

# USE AT YOUR OWN RISK 

# This tool converts a shell script into a SETUID script that is owned by root 

This project provides a collection of shell scripts wrapped into SUID binaries using `shc` (Shell Script Compiler). This allows unprivileged users to execute specific system tasks or switch to the `ansible` user environment without needing to use `sudo` directly for each command.

## Overview

The tools in this repository follow a pattern of wrapping a simple shell script into a C program, compiling it into a binary, and setting the Setuid (SUID) bit. When these binaries are owned by root, they execute with root privileges regardless of the user who invokes them.

### Included Tools

- **Ansible Wrappers**: `global-uptime`, `global-diskuse`, and `global-ping`. These scripts execute commands as the `ansible` user.
- **System Wrappers**: `system-reboot` (triggers an immediate reboot) and `system-upgrade` (runs `apt-get update && apt-get upgrade`).

## Prerequisites

- **shc**: The Shell Script Compiler must be installed on your system.
- **make**: Used for automating the build and installation process.
- **sudo**: Required for the installation phase to set root ownership and SUID permissions.

## Installation

To build and install the default set of tools (`global-uptime`, `global-diskuse`, `global-ping`) to `/usr/local/bin/`, run:

```bash
sudo make all
```

To install specific system tools:

```bash
sudo make system-reboot
sudo make system-upgrade
```

## Makefile Targets

| Target | Description | Installed Path |
|:-------|:------------|:---------------|
| `all` | Builds and installs `global-uptime`, `global-diskuse`, and `global-ping`. | `/usr/local/bin/` |
| `global-uptime` | Wraps `global-uptime.sh`. Runs `global-uptime` via `su - ansible`. | `/usr/local/bin/global-uptime` |
| `global-diskuse` | Wraps `global-diskuse.sh`. Runs `global-diskuse` via `su - ansible`. | `/usr/local/bin/global-diskuse` |
| `global-ping` | Wraps `global-ping.sh`. Runs `global-ping` via `su - ansible`. | `/usr/local/bin/global-ping` |
| `system-reboot` | Wraps `system-reboot.sh`. Executes `reboot now`. | `/usr/local/bin/system-reboot` |
| `system-upgrade` | Wraps `system-upgrade.sh`. Executes `apt-get update && apt-get upgrade`. | `/usr/local/bin/system-upgrade` |
| `clean` | Removes local binaries, generated C source files, and uninstalls core tools. | N/A |

## Usage

Once installed, any user with execution permissions can run the tools directly:

```bash
global-uptime
system-upgrade
```

## Security Considerations

- **SUID Root**: These binaries run with root privileges. They are designed to allow specific actions without granting full `sudo` access.
- **shc**: While `shc` provides some obfuscation, it is not a substitute for robust security. Ensure the source scripts do not contain sensitive information.
- **Permissions**: The `Makefile` sets the SUID bit and assumes root ownership. Review the `Makefile` if you need to restrict execution to a specific group.
