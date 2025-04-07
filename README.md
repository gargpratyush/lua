# Lua Notifier Kernel Module

A Linux kernel module that provides a character device interface for capturing and storing messages. This module can be used to monitor and log kernel messages through a user-space interface.


![luanotifier-img (1)](https://github.com/user-attachments/assets/1f434c2b-2451-42f4-958c-4e4fce3ee9a5)

![luanotifier-img (2)](https://github.com/user-attachments/assets/f5c89417-0458-45db-af56-5689e871a9eb)

## Features

- Character device interface at `/dev/luanotifier`
- Thread-safe message storage
- Support for both read and write operations
- Debug logging through kernel messages
- Configurable buffer size for messages

## Note

- Root/sudo access for module loading is required.

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd lua
```

2. Build the module:
```bash
make -f kbuild.mk clean
make -f kbuild.mk
```

3. Load the module:
```bash
sudo insmod luanotifier.ko
```

## Usage

### Writing Messages
```bash
# Write a message to the device
echo "Your message" | sudo tee /dev/luanotifier
```

### Reading Messages
```bash
# Read all stored messages
sudo cat /dev/luanotifier
```

### Monitoring Kernel Messages
```bash
# View module debug messages
sudo dmesg | grep "Lua Notifier"
```

## Module Details

### Device Information
- Device Name: `luanotifier`
- Major Number: Dynamically allocated
- Minor Number: 0
- Device Path: `/dev/luanotifier`

### Configuration
- Maximum Events: 100
- Maximum Event Size: 256 bytes

## Development

### Building
```bash
# Clean previous builds
make -f kbuild.mk clean

# Build the module
make -f kbuild.mk
```

### Loading/Unloading
```bash
# Load the module
sudo insmod luanotifier.ko

# Unload the module
sudo rmmod luanotifier
```

### Debugging
```bash
# View kernel messages
sudo dmesg | tail

# Check module status
lsmod | grep luanotifier
```
