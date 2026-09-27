# WiFi File Transfer — macOS 📡

Transfer files between your Mac, phone, and other devices on the same WiFi network.  
No cables, no cloud, no accounts — just a URL.

## 🚀 Quick Start

```bash
# 1. Clone
git clone https://github.com/TJeyesh/wifi-transfer-mac.git
cd wifi-transfer-mac

# 2. Create virtual environment & install dependencies
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# 3. Run
chmod +x server.sh
./server.sh start
```

### Transfer Files

1. Open the **Network URL** shown in terminal on any device on the same WiFi
2. Upload files via drag & drop, or use the **⚡ Fast Upload** for large files
3. Download files from the file list

## ✨ Features

- **📱 Cross-device** — Share files between your phone, iPad, and Mac
- **⚡ Fast Upload** — Direct HTTP upload endpoint bypasses Streamlit for maximum speed
- **📷 QR Code** — Scan to open on your phone instantly
- **🔒 Local only** — Files never leave your network
- **🎨 Beautiful UI** — Modern dark theme with glassmorphism

## 📋 Commands

```bash
./server.sh start       # Start the server
./server.sh stop        # Stop the server
./server.sh restart     # Restart the server
./server.sh status      # Check if the server is running
./server.sh             # Interactive menu
```

## 🏗️ Architecture

| Component | Port | Purpose |
|-----------|------|---------|
| Streamlit App | 8501 | Main UI — file list, QR codes, upload |
| File Server | 8502 | Direct HTTP downloads + Fast Upload |

### Fast Upload (Port 8502)

For large files, the **Fast Upload** page at `http://<your-ip>:8502/upload` bypasses Streamlit entirely:
- Raw HTTP POST — no multipart encoding overhead
- Streams directly to disk in 256 KB chunks
- Multi-threaded — parallel uploads/downloads
- Real-time speed indicator and progress bars

## 📁 Project Structure

```
wifi-transfer-mac/
├── app.py                # Main Streamlit application
├── server.sh             # macOS launcher script
├── requirements.txt      # Python dependencies
├── .streamlit/
│   └── config.toml       # Streamlit configuration
└── static/               # Uploaded files stored here (git-ignored)
```

## ⚙️ Requirements

- **Python 3.8+** (pre-installed on macOS, or `brew install python`)
- Both devices must be on the **same WiFi network**

### Troubleshooting

- If macOS blocks the script: `chmod +x server.sh`
- If ports are in use: check with `lsof -i :8501` and kill the process
- Firewall prompt: Allow incoming connections for Python

## 📄 License

MIT
