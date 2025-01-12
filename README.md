# Frida Sign Hook Generator

A powerful Android security research tool that automatically generates Frida scripts for signature and security bypass operations. This tool extracts APK signatures and creates custom hooks to bypass signature verification, security checks, and API protections.

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.6%2B-blue)](https://www.python.org/downloads/)
## Watch the Video

[![YouTube Video](https://img.youtube.com/vi/qrC0qOCZ3DQ/0.jpg)](https://youtu.be/qrC0qOCZ3DQ?si=5lJZBaH00jvJ-eJ1)

[Click here to watch the video on YouTube](https://youtu.be/qrC0qOCZ3DQ?si=5lJZBaH00jvJ-eJ1)


## 📱 Features

- Automatic APK signature extraction
- Custom Frida script generation
- Multiple certificate format support (RSA, DSA, EC)
- Security verification bypass
- API key protection bypass
- Package name detection
- MessageDigest bypass
- Java Security signature bypass

## ⚙️ Requirements

### System Requirements
```bash
# Ubuntu/Debian
sudo apt-get update
sudo apt-get install python3 python3-pip openssl android-sdk-build-tools adb

# Arch Linux
sudo pacman -S python python-pip openssl android-sdk-build-tools android-tools

# macOS
brew install python3 openssl android-sdk-build-tools android-platform-tools
```

### Python Requirements
```
frida-tools>=12.0.0
hexdump>=3.3.0
construct>=2.10.0
colorama>=0.4.6
```

## 📥 Installation

1. Clone the repository:
```bash
git clone https://github.com/riyadmondol2006/Frida-Sign-Hook-Generator.git
cd Frida-Sign-Hook-Generator
```

2. Install requirements:
```bash
pip3 install -r requirements.txt
```

## 🔧 Device Setup

1. Enable Developer Mode & USB Debugging:
   - Go to Settings → About Phone
   - Tap Build Number 7 times
   - Go back to Settings → Developer Options
   - Enable USB Debugging

2. Download Frida Server:
   - Get latest version from [Frida Releases](https://github.com/frida/frida/releases)
   - Choose correct architecture:
     - arm64: Modern Android phones
     - arm: Older 32-bit phones
     - x86_64: x64 emulators
     - x86: 32-bit emulators

3. Setup Frida Server:
```bash
# Check device connection
adb devices

# Push frida-server
adb push frida-server /data/local/tmp/
adb shell "chmod 755 /data/local/tmp/frida-server"
```

## 🚀 Usage

1. Start Frida Server:
```bash
# Root required
adb shell "su -c '/data/local/tmp/frida-server &'"
```

2. Generate Script:
```bash
python3 run.py path/to/your.apk
```

3. Deploy & Run:
```bash
# Push generated script
adb push frida_[package_name].js /data/local/tmp/

# Run with Frida
frida -U -l /data/local/tmp/frida_[package_name].js -f [package_name]
```

## ✅ Successful Output

When everything works correctly, you'll see:
```
>> start
>> api.init
>> sig.init
>> sec.init
>> done
```

## 🔍 How It Works

The tool performs these operations:
1. Extracts the target APK's signature
2. Detects the package name
3. Generates a custom Frida script that:
   - Hooks signature verification methods
   - Bypasses security checks
   - Handles API key protection
   - Implements MessageDigest bypass

## ❗ Troubleshooting

### Frida Server Issues
```bash
# Check if running
adb shell ps | grep frida

# Restart server
adb shell "su -c 'killall frida-server'"
adb shell "su -c '/data/local/tmp/frida-server &'"
```

### Device Connection
```bash
# Restart ADB
adb kill-server
adb start-server
adb devices
```

### Permission Problems
```bash
# Check root
adb shell su

# Verify permissions
adb shell "ls -l /data/local/tmp/frida-server"
```

### Common Errors

1. "Device not found":
   - Check USB debugging is enabled
   - Restart ADB server
   - Try different USB cable/port

2. "Frida server not running":
   - Verify device is rooted
   - Check correct architecture version
   - Kill and restart frida-server

3. "Script injection failed":
   - Verify package name
   - Check if app is installed
   - Confirm frida-server is running

## ⚠️ Important Notes

1. Root Access Required:
   - Device must be rooted
   - Su binary must be available
   - Root manager must grant permissions

2. Compatibility:
   - Android 5.0+ supported
   - Both ARM and x86 architectures
   - Works with most root solutions

3. Limitations:
   - Some apps may have additional protections
   - Root detection might need additional bypass
   - Custom ROM might affect functionality

## 📚 Advanced Usage

1. Custom Hook Modifications:
```javascript
class CustomHooks {
    static init() {
        try {
            // Add your custom hooks here
        } catch (e) { err("custom.fail", e) }
    }
}
```

2. Multiple APK Processing:
```bash
for apk in *.apk; do
    python3 run.py "$apk"
done
```

## ⚖️ Legal Disclaimer

This tool is for educational and research purposes only. Users are responsible for compliance with local laws and regulations. The creator is not responsible for any misuse or damage.

## 👥 Contact & Support

Created by: Riyad M
- Telegram: [@riyadmondol2006](https://t.me/riyadmondol2006)
- GitHub: [@riyadmondol2006](https://github.com/riyadmondol2006)
- YouTube: [@reversesio](https://youtube.com/@reversesio)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
Made with ❤️ by Riyad M
