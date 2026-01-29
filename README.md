# 👻 Ghostmove

**Zero-dependency cross-platform mouse control using native OS APIs**

A lightweight post-exploitation research tool for testing endpoint detection and response (EDR) capabilities against dependency-free payloads.

[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS-blue)]()
[![Python](https://img.shields.io/badge/python-3.7+-green)]()
[![Dependencies](https://img.shields.io/badge/dependencies-0-brightgreen)]()
[![License](https://img.shields.io/badge/license-MIT-blue)]()

---

## 🎯 Overview

Ghostmove provides programmatic mouse control across Windows, Linux, and macOS **without any external dependencies**. Built using direct OS API bindings via Python's `ctypes`, this tool demonstrates how to interact with low-level system interfaces for red team operations.

### Why This Exists

Traditional automation libraries (PyAutoGUI, pyautogui, etc.) require pip installation and create large dependency trees - easily detected by EDR solutions. This project explores minimal-footprint cursor control using only Python standard library + native OS APIs.

**Use Cases:**
- Red Team: Post-exploitation persistence testing
- Blue Team: Understanding evasion techniques for better detection
- Research: EDR bypass methodology
- Education: Learning OS API interaction

---

## ⚡ Features

### Multi-Platform Support
- **Windows**: Direct `user32.dll` bindings (SetCursorPos, GetCursorPos)
- **Linux X11**: `libX11.so` integration (XWarpPointer, XQueryPointer)
- **macOS**: Quartz/CoreGraphics (CGEventCreateMouseEvent)

### Movement Patterns
- `jitter` - Random micro-movements (simulates hardware glitch)
- `drift` - Slow movement toward screen corners
- `circle` - Circular motion patterns
- `evasion` - Cursor jumps away when user moves it
- `drunk` - Wobbly, erratic movements
- `gravity` - Constant pull toward screen center
- `chaos` - Randomly switches between all patterns

### Zero Dependencies
- Pure Python 3.7+ (no pip install required)
- Works with standard library only
- Entire payload: ~15KB
- Runs in restricted/air-gapped environments

---

## 🚀 Quick Start

### Installation
```bash
git clone https://github.com/YOUR_USERNAME/phantom-cursor.git
cd phantom-cursor
```

No `pip install` needed!

### Basic Usage
```bash
# Random jitter for 60 seconds
python phantom_cursor.py --mode jitter --duration 60

# Drift to bottom-right corner
python phantom_cursor.py --mode drift --duration 30

# Evasion mode (cursor runs from user)
python phantom_cursor.py --mode evasion --duration 120

# Chaos mode (random patterns)
python phantom_cursor.py --mode chaos --duration 60
```

### Programmatic Usage
```python
from phantom_cursor import get_cursor_controller

# Get platform-appropriate controller
cursor = get_cursor_controller()

# Move to absolute position
cursor.move_to(500, 300)

# Move relative to current position
cursor.move_relative(10, -20)

# Get current position
x, y = cursor.get_position()

# Get screen dimensions
width, height = cursor.get_screen_size()
```

---

## 🛡️ Detection & Evasion

### What EDR Solutions See

**Traditional automation (PyAutoGUI):**
```
Process: python.exe
Loaded modules: pyautogui.pyd, PIL.pyd, numpy.pyd, ...
Signature: Known automation library
Detection: ✅ Flagged immediately
```

**Ghostmove:**
```
Process: python.exe
Loaded modules: ctypes (standard library)
Signature: Direct OS API calls (legitimate use)
Detection: ⚠️ Requires behavioral analysis
```

### Defensive Perspective

**Blue team should monitor:**
- Unusual cursor movement patterns (velocity, acceleration analysis)
- Cursor activity when user input devices are idle
- Process making excessive cursor API calls
- Correlation with other suspicious behaviors

**Detection strategies:**
- Behavioral analysis (movement pattern recognition)
- User input device correlation (keyboard/mouse hardware events)
- Process reputation and parent process analysis

---

## 📋 Technical Details

### Windows Implementation
Uses `ctypes.windll.user32`:
- `SetCursorPos(x, y)` - Absolute positioning
- `GetCursorPos(POINT*)` - Current position
- `GetSystemMetrics()` - Screen dimensions

### Linux X11 Implementation
Uses `libX11.so` via ctypes:
- `XWarpPointer()` - Cursor movement
- `XQueryPointer()` - Position retrieval
- `XDisplayWidth/Height()` - Screen size

### macOS Implementation  
Uses Quartz framework:
- `CGEventCreateMouseEvent()` - Create mouse event
- `CGEventPost()` - Post event to system
- `CGEventGetLocation()` - Get cursor position

---

## ⚠️ Disclaimer

**FOR EDUCATIONAL AND AUTHORIZED TESTING ONLY**

This tool is provided for:
- Security research
- Authorized penetration testing
- Educational purposes
- Red team exercises with proper authorization

**Unauthorized use is illegal and unethical.**

Always obtain written permission before testing on systems you don't own.

---

## 🤝 Contributing

Contributions welcome! Areas for improvement:
- Wayland support for modern Linux
- Additional movement patterns
- Stealth/evasion improvements
- Detection bypass techniques
- Performance optimizations

**Contribution to:** [100 Red Team Projects](https://github.com/kurogai/100-redteam-projects)

---

## 📝 License

MIT License - See [LICENSE](LICENSE) file for details

---

## 👤 Author

**Manthan Ghasadiya**
- GitHub: [@manthanghasadiya](https://github.com/manthanghasadiya)
- LinkedIn: [Manthan Ghasadiya](https://linkedin.com/in/manthanghasadiya)
- Security Analyst @ Jacobian Engineering

---

## 🔗 Related Work

- [eBPF-based Ransomware Detection](link-when-you-publish-it)
- [100 Red Team Projects](https://github.com/kurogai/100-redteam-projects)

---

## 📚 References

- [Windows User32 API Documentation](https://learn.microsoft.com/en-us/windows/win32/api/winuser/)
- [X11 API Reference](https://www.x.org/releases/current/doc/libX11/libX11/libX11.html)
- [Quartz Event Services](https://developer.apple.com/documentation/coregraphics/quartz_event_services)

---

**Built with ❤️ for the red team community**
