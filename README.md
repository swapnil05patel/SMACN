# SMACN - Secure Mobile Ad-Hoc Communication Network

A modern, real-time communication platform for mobile ad-hoc networks with advanced monitoring, broadcasting, and network analytics capabilities.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [API Endpoints](#api-endpoints)
- [Configuration](#configuration)
- [Network Analysis with Wireshark](#-network-analysis-with-wireshark)
- [Network Simulation with Cisco Packet Tracer](#-network-simulation-with-cisco-packet-tracer)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#contributing)

## 🎯 Overview

SMACN is a comprehensive solution for establishing secure, decentralized communication networks between mobile devices without requiring a central server. It provides real-time messaging, network monitoring, and device discovery capabilities with an intuitive web-based dashboard.

The platform is designed for scenarios where traditional network infrastructure is unavailable or unreliable, such as:
- Emergency response operations
- Remote field operations
- Disaster recovery communications
- Military/tactical communications
- IoT device networks

## ✨ Features

### Core Functionality
- **Device Discovery**: Automatic detection and registration of connected devices
- **Real-time Messaging**: Instant message delivery between network nodes
- **Multi-Channel Broadcasting**: Send messages across different priority channels (Emergency, Info, Chat)
- **Secure Communication**: End-to-end encryption for all messages
- **Network Monitoring**: Real-time tracking of network health and performance

### Dashboard Features
- **Live Statistics**: Connected devices, network latency, and traffic monitoring
- **Performance Graphs**: Real-time trend visualization for latency, traffic, and device count
- **Message History**: Complete broadcast message log with sender and timestamp information
- **Network Logs**: Terminal-style live network activity logs
- **Responsive Design**: Works seamlessly on desktop, tablet, and mobile devices
- **Particle Background**: Animated particle effects for enhanced UI

### Broadcasting System
- **Channel-Based Messaging**: Organize messages by priority (Emergency, Info, Chat)
- **Sender Identification**: Track which device sent each message
- **Timestamps**: Precise message timing for audit trails
- **Message History**: Access to all broadcast messages in the network

## 🏗️ Architecture

### Backend Architecture
```
Backend (Flask + SocketIO)
├── Server Management
├── Device Connection Handling
├── Message Routing
├── Encryption/Decryption
├── Network Monitoring
└── Data Persistence
```

### Frontend Architecture
```
Frontend (Next.js + React)
├── Dashboard
│   ├── Statistics Cards
│   ├── Performance Charts
│   └── Network Metrics
├── Broadcast System
│   ├── Message Composer
│   ├── Channel Selection
│   └── Message Display
├── Network Logs
└── Responsive Sidebar Navigation
```

## 🛠️ Tech Stack

### Backend
- **Framework**: Flask with Flask-SocketIO
- **Real-time Communication**: Socket.IO
- **Encryption**: Custom encryption module
- **Language**: Python 3.8+
- **Server**: Eventlet WSGI

### Frontend
- **Framework**: Next.js 16.1.6
- **UI Library**: React 18.2.0
- **Charts**: Chart.js with react-chartjs-2
- **Real-time Client**: Socket.IO Client
- **HTTP Client**: Axios
- **Styling**: CSS-in-JS

### Database
- In-memory storage (can be extended to persistent storage)

## 📦 Installation

### Prerequisites
- Python 3.8 or higher
- Node.js 16 or higher
- npm or yarn

### Backend Setup

1. Navigate to the backend directory:
```bash
cd backend
```

2. Create a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Run the backend server:
```bash
python server.py
```

The backend will start on `http://0.0.0.0:8000`

### Frontend Setup

1. Navigate to the frontend directory:
```bash
cd frontend/react_app
```

2. Install dependencies:
```bash
npm install
```

3. Update the API base URL in `pages/index.js`:
```javascript
const API_BASE = "http://YOUR_BACKEND_IP:8000";
```

4. Run the development server:
```bash
npm run dev
```

The frontend will be available at `http://localhost:3000`

## 🚀 Usage

### Starting the Application

1. **Start Backend Server**:
```bash
cd backend
python server.py
```

2. **Start Frontend Server** (in another terminal):
```bash
cd frontend/react_app
npm run dev
```

3. **Access Dashboard**:
Open your browser and navigate to `http://localhost:3000`

### Using the Dashboard

#### Dashboard Tab
- View real-time network statistics
- Monitor connected devices
- Track network latency and traffic
- View performance trends with interactive charts

#### Broadcasts Tab
- Select a broadcast channel (Emergency, Info, Chat)
- Compose and send messages
- View all messages from all devices
- See sender information and timestamps

#### Logs Tab
- Monitor network activity in real-time
- View connection/disconnection events
- Track broadcast messages
- Debug network issues

## 📁 Project Structure

```
SMACN/
├── backend/
│   ├── server.py              # Main Flask server
│   ├── encryption.py          # Encryption utilities
│   ├── device_discovery.py    # Device discovery logic
│   ├── routing.py             # Message routing
│   ├── utils.py               # Utility functions
│   ├── client.py              # Client implementation
│   └── requirements.txt        # Python dependencies
│
├── frontend/
│   └── react_app/
│       ├── pages/
│       │   └── index.js        # Main dashboard page
│       ├── src/
│       │   ├── components/     # React components
│       │   ├── services/       # API services
│       │   └── App.js          # App component
│       ├── package.json        # Node dependencies
│       └── next.config.js      # Next.js configuration
│
└── README.md                   # This file
```

## 🔌 API Endpoints

### HTTP Endpoints

#### GET /status
Returns current network status and statistics.

**Response**:
```json
{
  "devices": 3,
  "latency": 15,
  "traffic": 256,
  "logs": ["[CONNECT] Device connected", ...],
  "broadcasts": [{"message": "...", "channel": "emergency", ...}]
}
```

#### POST /broadcast
Send a broadcast message to all connected devices.

**Request Body**:
```json
{
  "message": "Emergency alert",
  "channel": "emergency",
  "sender_sid": "socket_id",
  "timestamp": "14:30:45"
}
```

#### GET /stats
Returns detailed network statistics including per-device metrics.

### WebSocket Events

#### Client → Server
- `connect`: Device connects to network
- `register_device`: Register device with IP
- `message`: Send encrypted message
- `ping_response`: Respond to latency ping
- `broadcast`: Receive broadcast message

#### Server → Client
- `device_list`: Updated list of connected devices
- `ping_request`: Latency measurement request
- `broadcast`: Incoming broadcast message
- `log_update`: Network log updates

## ⚙️ Configuration

### Backend Configuration

Edit `backend/server.py` to modify:
- Server host and port
- CORS settings
- SocketIO configuration
- Encryption parameters

### Frontend Configuration

Edit `frontend/react_app/pages/index.js` to modify:
- Backend API URL
- Device IP address
- Polling intervals
- Chart update frequency

## 🔐 Security Features

- **End-to-End Encryption**: All messages are encrypted using custom encryption
- **Device Authentication**: Socket-based device identification
- **CORS Protection**: Cross-origin requests are controlled
- **Secure WebSocket**: Support for WSS (WebSocket Secure)

## 📊 Monitoring & Analytics

- **Real-time Metrics**: Live device count, latency, and traffic
- **Historical Data**: 20-point history for trend analysis
- **Network Logs**: Complete audit trail of network events
- **Performance Graphs**: Visual representation of network health

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🔍 Network Analysis with Wireshark

### What is Wireshark?
Wireshark is a free, open-source network protocol analyzer that captures and displays data traveling back and forth on a network in real-time.

### Installation Steps

**Windows**:
1. Visit https://www.wireshark.org/download/
2. Download "Wireshark x.x.x Installer (64-bit)"
3. Run the installer
4. Follow the installation wizard
5. Install Npcap when prompted
6. Complete installation

**macOS**:
```bash
brew install wireshark
```

**Linux (Ubuntu/Debian)**:
```bash
sudo apt-get install wireshark
sudo usermod -a -G wireshark $USER
```

### Practical Steps to Capture SMACN Traffic

#### Step 1: Prepare Your Environment
```bash
# Terminal 1: Start Backend Server
cd backend
python server.py
# Output: Running on http://0.0.0.0:8000

# Terminal 2: Start Frontend
cd frontend/react_app
npm run dev
# Output: ▲ Next.js 16.1.6 ready on http://localhost:3000
```

#### Step 2: Open Wireshark
- **Windows**: Click Start → Search "Wireshark" → Open
- **macOS**: Open Applications → Wireshark
- **Linux**: Open terminal → `wireshark`

#### Step 3: Select Network Interface
1. When Wireshark opens, you'll see a list of network interfaces
2. Look for your active network interface:
   - **Windows**: "Ethernet" or "Wi-Fi"
   - **macOS**: "en0" or "en1"
   - **Linux**: "eth0" or "wlan0"
3. Double-click on the interface to start capturing

#### Step 4: Start Capturing Packets
- You should see packets appearing in real-time
- The interface shows:
  - **No.**: Packet number
  - **Time**: Timestamp
  - **Source**: Source IP
  - **Destination**: Destination IP
  - **Protocol**: TCP, HTTP, WebSocket, etc.
  - **Length**: Packet size in bytes
  - **Info**: Brief description

#### Step 5: Generate SMACN Traffic
Open your browser and navigate to `http://localhost:3000`

**Perform these actions**:
1. Wait for dashboard to load (generates GET /status requests)
2. Send a broadcast message:
   - Select channel: "Emergency"
   - Type message: "Test broadcast message"
   - Click "Send"
3. Connect another device (open another browser tab)
4. Send more messages from different channels

#### Step 6: Filter Traffic to See Only SMACN

In Wireshark, type in the filter box at the top:

**Filter 1: See all traffic on port 8000**
```
tcp.port == 8000
```
Press Enter. Now you'll only see SMACN-related traffic.

**Filter 2: See only HTTP POST requests (broadcasts)**
```
http.request.method == "POST"
```

**Filter 3: See only WebSocket traffic**
```
websocket
```

**Filter 4: See traffic from specific IP**
```
ip.src == 127.0.0.1 || ip.dst == 127.0.0.1
```

#### Step 7: Examine a Broadcast Message

1. In the packet list, find a POST request to `/broadcast`
2. Click on it to select it
3. In the middle panel, expand:
   - **Frame**: Shows packet size and timing
   - **Ethernet II**: Shows MAC addresses
   - **Internet Protocol Version 4**: Shows source/destination IPs
   - **Transmission Control Protocol**: Shows port numbers
   - **Hypertext Transfer Protocol**: Shows HTTP headers and method
4. Scroll down to see the **Message Body** containing your broadcast JSON

**Example JSON you'll see**:
```json
{
  "message": "Test broadcast message",
  "channel": "emergency",
  "sender_sid": "pTW57lq2U54_C-DfAAAH",
  "timestamp": "14:30:45"
}
```

#### Step 8: Follow a Complete TCP Stream

1. Right-click on any packet related to your broadcast
2. Select "Follow" → "TCP Stream"
3. A new window opens showing the complete conversation:
   - Client request (top, in red)
   - Server response (bottom, in blue)
4. You can see the entire HTTP exchange

#### Step 9: Analyze Latency

1. Filter for ping requests:
```
tcp.port == 8000 && websocket
```

2. Look for packets with "ping_request" in the info
3. Right-click → "Set Time Reference"
4. Find the corresponding "ping_response"
5. The time difference = latency

#### Step 10: Export Captured Data

1. Go to **File** → **Export Specified Packets**
2. Choose format:
   - **pcapng**: Recommended (preserves all data)
   - **pcap**: Standard format
3. Save with filename: `smacn_capture.pcapng`
4. Click "Save"

### What to Look For in Wireshark

| What | Where to Find | What It Means |
|------|---------------|--------------|
| **Device Connection** | TCP SYN packets to port 8000 | Device joining network |
| **Broadcast Message** | POST /broadcast in HTTP | Message being sent |
| **Status Update** | GET /status in HTTP | Dashboard polling |
| **Latency Ping** | WebSocket frames | Network latency measurement |
| **Device Disconnect** | TCP FIN/RST packets | Device leaving network |
| **Encrypted Data** | Binary data in payload | Encrypted message content |

### Common Issues and Solutions

**Issue**: No packets appearing
- **Solution**: Make sure you selected the correct network interface
- **Solution**: Ensure SMACN is running and generating traffic

**Issue**: Can't see HTTP payload
- **Solution**: Make sure you're capturing on the correct interface
- **Solution**: Try filtering: `http.request.method == "POST"`

**Issue**: Too many packets
- **Solution**: Use filters to narrow down
- **Solution**: Stop capture, clear packets, restart

---

## 🌐 Network Simulation with Cisco Packet Tracer

### What is Cisco Packet Tracer?
Cisco Packet Tracer is a network simulation software that allows you to design, configure, and troubleshoot networks in a virtual environment.

### Installation Steps

1. Visit https://www.netacad.com/portal/resources/packet-tracer
2. Create a free Cisco Networking Academy account
3. Download Packet Tracer for your OS
4. Install the application
5. Launch Packet Tracer

### Practical Steps to Simulate SMACN Network

#### Step 1: Create a New Project
1. Open Cisco Packet Tracer
2. Click **File** → **New**
3. You'll see an empty canvas

#### Step 2: Add Network Devices

**Add 3 PCs (Client Devices)**:
1. On the left panel, click **End Devices** (computer icon)
2. Drag **PC** onto the canvas 3 times
3. Position them in a triangle formation
4. Label them:
   - PC1 (top-left)
   - PC2 (top-right)
   - PC3 (bottom)

**Add 1 Switch**:
1. Click **Switches** category
2. Drag **2960 Switch** to the center
3. Label it "Switch-1"

**Add 1 Server (Optional)**:
1. Click **End Devices**
2. Drag **Server** to the canvas
3. Label it "Backend-Server"

#### Step 3: Connect Devices with Cables

1. Click **Connections** (lightning bolt icon)
2. Select **Copper Straight-Through** cable
3. Connect each PC to the Switch:
   - Click on PC1 → Click on Switch
   - Click on PC2 → Click on Switch
   - Click on PC3 → Click on Switch
4. Connect Server to Switch:
   - Click on Server → Click on Switch

**Your topology should look like**:
```
    PC1 ─┐
         ├─ Switch ─ Server
    PC2 ─┤
         │
    PC3 ─┘
```

#### Step 4: Configure IP Addresses

**For PC1**:
1. Double-click on PC1
2. Click **Desktop** tab
3. Click **IP Configuration**
4. Select **Static**
5. Enter:
   - IP Address: `192.168.1.10`
   - Subnet Mask: `255.255.255.0`
6. Close the window

**For PC2**:
1. Double-click on PC2
2. Repeat steps 2-5
3. Enter:
   - IP Address: `192.168.1.11`
   - Subnet Mask: `255.255.255.0`

**For PC3**:
1. Double-click on PC3
2. Repeat steps 2-5
3. Enter:
   - IP Address: `192.168.1.12`
   - Subnet Mask: `255.255.255.0`

**For Server**:
1. Double-click on Server
2. Click **Desktop** tab
3. Click **IP Configuration**
4. Enter:
   - IP Address: `192.168.1.100`
   - Subnet Mask: `255.255.255.0`

#### Step 5: Test Connectivity

**Ping from PC1 to PC2**:
1. Double-click on PC1
2. Click **Desktop** tab
3. Click **Command Prompt**
4. Type: `ping 192.168.1.11`
5. Press Enter
6. You should see: `Reply from 192.168.1.11: bytes=32 time=0ms TTL=64`

**Ping from PC1 to Server**:
1. In the same Command Prompt
2. Type: `ping 192.168.1.100`
3. Press Enter
4. Should get successful replies

#### Step 6: Enable Simulation Mode

1. At the bottom right, click **Simulation** button
2. The interface changes to show simulation controls
3. You'll see a "Simulation Panel" on the right

#### Step 7: Simulate SMACN Backend Server

1. Double-click on **Server**
2. Click **Services** tab
3. Click **HTTP**
4. Enable HTTP service:
   - Check the "On" checkbox
5. Close the window

#### Step 8: Simulate Device Communication

**Scenario 1: Send Message from PC1 to Server**

1. In Simulation mode, click **Add Complex PDU** button
2. Select **PC1** as source
3. Select **Server** as destination
4. In the dialog:
   - Source Port: `12345`
   - Destination Port: `8000`
   - Protocol: `TCP`
5. Click **Create PDU**

#### Step 9: Capture and View Packets

1. Click **Capture/Forward** button to send the packet
2. Watch the packet travel from PC1 → Switch → Server
3. The packet appears as a colored box moving through the network
4. Click on the packet to see details:
   - Source IP: 192.168.1.10
   - Destination IP: 192.168.1.100
   - Protocol: TCP
   - Port: 8000

#### Step 10: Simulate Network Failure

**Scenario: Device Disconnection**

1. Right-click on **PC2**
2. Select **Turn Off**
3. Notice PC2 goes offline (grayed out)
4. Try to ping PC2 from PC1:
   - Double-click PC1
   - Command Prompt
   - `ping 192.168.1.11`
   - You'll get "Destination host unreachable"
5. Right-click PC2 → **Turn On** to restore

**Scenario: Link Failure**

1. Right-click on the cable between PC3 and Switch
2. Select **Delete**
3. PC3 is now disconnected
4. Try to ping PC3 from PC1 - it will fail
5. Right-click on Switch → **Add Connection** to restore

#### Step 11: Monitor Network Statistics

1. Click **Simulation** menu
2. Select **Show Counters**
3. A panel appears showing:
   - Packets sent/received
   - Bytes transferred
   - Errors
4. Send multiple PDUs and watch counters increase

#### Step 12: Advanced Scenario - Multi-Device Broadcast

1. Create PDUs from PC1 to all other devices:
   - PC1 → PC2
   - PC1 → PC3
   - PC1 → Server
2. Click **Capture/Forward** multiple times
3. Watch all packets traverse the network
4. Observe how the Switch forwards packets

#### Step 13: View Detailed Packet Information

1. In Simulation mode, click on a packet in transit
2. A popup shows:
   - **PDU Information**: Source, destination, protocol
   - **Outgoing PDU Details**: Current hop
   - **Device Information**: Which device is processing it
3. Click **Next Layer** to see protocol details

#### Step 14: Generate Traffic Report

1. Send multiple PDUs (at least 10)
2. Go to **Simulation** → **Show Counters**
3. Take a screenshot showing:
   - Total packets sent
   - Total bytes transferred
   - Success rate
4. Document findings

#### Step 15: Save Your Project

1. Click **File** → **Save**
2. Name it: `SMACN_Network_Simulation`
3. Choose location
4. Click **Save**

### Complete SMACN Simulation Checklist

- [ ] Created 3 PCs and 1 Server
- [ ] Connected all devices to Switch
- [ ] Configured all IP addresses correctly
- [ ] Tested ping between all devices
- [ ] Enabled Simulation mode
- [ ] Created PDUs between devices
- [ ] Captured and viewed packet details
- [ ] Simulated device disconnection
- [ ] Simulated link failure
- [ ] Monitored network statistics
- [ ] Generated traffic report
- [ ] Saved the project

### Expected Results

**Successful Simulation Should Show**:
- ✅ All devices can communicate
- ✅ Packets travel through Switch
- ✅ Ping responses are successful
- ✅ PDUs are delivered correctly
- ✅ Network recovers from failures
- ✅ Statistics show traffic flow

### Troubleshooting Cisco Packet Tracer

| Problem | Solution |
|---------|----------|
| Devices can't ping | Check IP addresses and subnet masks |
| Packets not moving | Make sure Simulation mode is enabled |
| No statistics | Click "Show Counters" in Simulation menu |
| Connection failed | Verify cables are connected properly |
| Server not responding | Check if HTTP service is enabled |

---

## 🆘 Troubleshooting

### Backend Connection Issues
- Ensure backend is running on the correct IP and port
- Check firewall settings
- Verify CORS configuration

### Frontend Not Showing Data
- Clear browser cache
- Check browser console for errors
- Verify API_BASE URL is correct
- Ensure backend is accessible

### Latency Shows 0
- Wait for ping responses (5-second intervals)
- Check network connectivity
- Verify ping_request/ping_response handlers

### Traffic Not Updating
- Send broadcast messages to generate traffic
- Check bytes_sent/bytes_received tracking
- Verify HTTP request tracking is enabled

## 📞 Support

For issues, questions, or suggestions, please open an issue on the project repository.

## 🎓 Learning Resources

- [Socket.IO Documentation](https://socket.io/docs/)
- [Flask Documentation](https://flask.palletsprojects.com/)
- [Next.js Documentation](https://nextjs.org/docs)
- [React Documentation](https://react.dev)

---

**SMACN** - Secure Mobile Ad-Hoc Communication Network v1.0.0

# SMACN
