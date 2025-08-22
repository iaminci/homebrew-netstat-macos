# netstat-macos

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Homebrew](https://img.shields.io/badge/Homebrew-formulae-orange)](https://brew.sh/)
[![macOS](https://img.shields.io/badge/macOS-compatible-brightgreen)](https://www.apple.com/macos/)

> Linux-compatible `netstat` replacement for macOS with full `-tulpn` support

Finally use `sudo netstat -tulpn` on macOS just like on Linux! This tool provides a Linux-compatible interface while preserving all native macOS netstat functionality.

## 🚀 Quick Start

```bash
# Install
brew tap yourusername/netstat-macos
brew install netstat-macos

# Use exactly like Linux
sudo netstat -tulpn
```

## 📋 Installation

### Requirements
- macOS 10.15 (Catalina) or later
- Homebrew installed ([Get Homebrew](https://brew.sh/))

### Install via Homebrew (Recommended)

```bash
# Add the tap
brew tap yourusername/netstat-macos

# Install the package
brew install netstat-macos

# Verify installation
netstat --version
```

### Manual Installation

```bash
# Download and install directly
curl -fsSL https://raw.githubusercontent.com/yourusername/homebrew-netstat-macos/main/install.sh | bash
```

## 🖥️ Usage

### Linux-Compatible Commands

All your favorite Linux netstat commands now work on macOS:

```bash
# Show all listening TCP and UDP ports with process info
sudo netstat -tulpn

# Show only TCP listening ports with process names
sudo netstat -tlp

# Show all connections with numerical addresses
netstat -an

# Show only UDP ports
netstat -un

# Show only listening ports
netstat -l
```

### Example Output

```bash
❯ sudo netstat -tulpn
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      423/sshd
tcp        0      0 127.0.0.1:5432          0.0.0.0:*               LISTEN      1234/postgres
tcp6       0      0 :::22                   :::*                    LISTEN      423/sshd
tcp6       0      0 :::80                   :::*                    LISTEN      567/nginx
udp        0      0 0.0.0.0:68              0.0.0.0:*                           890/dhclient
udp6       0      0 :::123                  :::*                                456/ntpd
```

### Native macOS Compatibility

All native macOS netstat features continue to work:

```bash
# Routing table
netstat -r

# Network interfaces  
netstat -i

# Network statistics
netstat -s

# Per-interface statistics
netstat -I en0
```

## ✨ Features

- ✅ **Full Linux Compatibility**: All `-tulpn` flags work exactly as expected
- ✅ **Process Information**: Shows PID and program names with `-p` flag
- ✅ **IPv6 Support**: Properly handles both IPv4 and IPv6 connections
- ✅ **Smart Fallback**: Automatically uses native macOS netstat for unsupported flags
- ✅ **No Breaking Changes**: Preserves all existing macOS netstat functionality
- ✅ **Secure**: Requires `sudo` for process information, just like Linux
- ✅ **Performance**: Lightweight wrapper with minimal overhead

## 🔄 Command Reference

### Linux-Style Options

| Flag | Description | Example |
|------|-------------|---------|
| `-t` | Show TCP connections | `netstat -t` |
| `-u` | Show UDP connections | `netstat -u` |
| `-l` | Show only listening ports | `netstat -l` |
| `-p` | Show process ID and name | `sudo netstat -p` |
| `-n` | Show numerical addresses | `netstat -n` |
| `-a` | Show all connections | `netstat -a` |

### Combined Options

| Command | Description |
|---------|-------------|
| `sudo netstat -tulpn` | Show all listening TCP/UDP ports with process info |
| `sudo netstat -tlp` | Show TCP listening ports with process names |
| `netstat -an` | Show all connections with numerical addresses |
| `sudo netstat -ulp` | Show UDP ports with process names |

### Native macOS Options

| Flag | Description |
|------|-------------|
| `-r` | Show routing table |
| `-i` | Show network interfaces |
| `-s` | Show network statistics |
| `-m` | Show memory statistics |

## 🆚 Comparison

### Before (macOS default)
```bash
❯ netstat -tulpn
netstat: n: unknown or uninstrumented protocol

❯ netstat -p tcp
netstat: option requires an argument -- p
```

### After (with netstat-macos)
```bash
❯ sudo netstat -tulpn
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.0.1:5432          0.0.0.0:*               LISTEN      1234/postgres
...
```

## 🔧 Troubleshooting

### Permission Issues
If you see permission warnings:
```bash
# The -p flag requires sudo for process information
sudo netstat -tulpn
```

### Command Not Found
If `netstat` still shows the old behavior:
```bash
# Clear shell cache
hash -r

# Or start a new shell session
exec zsh
```

### Verify Installation
```bash
# Check which netstat is being used
which netstat
# Should show: /opt/homebrew/bin/netstat

# Check version
netstat --version
# Should show: netstat-macos 1.0.0
```

### Restore Original netstat
```bash
# Uninstall netstat-macos
brew uninstall netstat-macos

# Remove the tap
brew untap yourusername/netstat-macos
```

## 🔄 Updates

```bash
# Update to latest version
brew update
brew upgrade netstat-macos

# Check for updates
brew outdated
```

## 🤝 Contributing

We welcome contributions! Here's how you can help:

1. **Report Issues**: Found a bug? [Open an issue](https://github.com/yourusername/homebrew-netstat-macos/issues)
2. **Feature Requests**: Want a new feature? [Request it here](https://github.com/yourusername/homebrew-netstat-macos/issues)
3. **Pull Requests**: Code improvements welcome!

### Development Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/homebrew-netstat-macos.git
cd homebrew-netstat-macos

# Test the formula
brew install --build-from-source Formula/netstat-macos.rb

# Run tests
brew test netstat-macos

# Audit the formula
brew audit --strict netstat-macos
```

## 📖 Why This Tool?

As developers, we often work across Linux servers and macOS development machines. The inconsistency in `netstat` behavior between these systems creates friction in our daily workflows. This tool eliminates that friction by providing the familiar Linux interface on macOS.

### Use Cases

- **DevOps Engineers**: Use the same commands across all systems
- **System Administrators**: Consistent network troubleshooting workflow  
- **Developers**: Debug local services with familiar Linux commands
- **Docker Users**: Monitor container networking with known commands
- **Security Professionals**: Network analysis with standard tooling

## 📚 Related Projects

- [iproute2mac](https://github.com/brona/iproute2mac) - Linux `ip` command for macOS
- [proctools](https://github.com/rgcr/proctools) - Linux `ps` improvements for macOS
- [gnu-sed](https://formulae.brew.sh/formula/gnu-sed) - GNU sed for macOS

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Thanks to the Homebrew team for the excellent package management system
- Inspired by the need for cross-platform consistency in system administration
- Built with ❤️ for the developer community

## 🔗 Links

- [Homebrew Formula](Formula/netstat-macos.rb)
- [Source Code](https://github.com/yourusername/netstat-macos-source)
- [Issue Tracker](https://github.com/yourusername/homebrew-netstat-macos/issues)
- [Homebrew Documentation](https://docs.brew.sh/)

---

<div align="center">

**Star ⭐ this repository if it helped you!**

[Report Bug](https://github.com/yourusername/homebrew-netstat-macos/issues) · [Request Feature](https://github.com/yourusername/homebrew-netstat-macos/issues) · [Contribute](https://github.com/yourusername/homebrew-netstat-macos/pulls)

</div>
