**📹 RealtimeWeb — Ứng dụng Gọi Video & Chat Thời Gian Thực**

Ứng dụng RealtimeWeb là một hệ thống gọi video/audio + chat thời gian thực được xây dựng bằng WebRTC, WebSocket (Python) và mã hóa AES động.
Dự án hỗ trợ truyền thông an toàn, xuyên NAT bằng STUN/TURN, và có thể hoạt động ngay trong mạng LAN hoặc Internet (qua ngrok/HTTPS).

**🚀 Tính năng chính**

🔊 Truyền video/audio thời gian thực qua WebRTC (SRTP + DTLS).

💬 Chat an toàn sử dụng WebRTC DataChannel.

🔐 Mã hóa AES-GCM động, tự xoay khóa theo thời gian.

🌐 Signaling server viết bằng Python (WebSocket + HTTP).

⚙️ Tự cấu hình STUN/TURN (coturn) để xuyên NAT.

💻 Chạy được ngay trên localhost hoặc mạng LAN.

📱 Hỗ trợ trình duyệt desktop/mobile (Chrome, Edge, Firefox).

**🏗️ Cấu trúc dự án**
RealtimeWeb/
├── statics/
│   └── diagram.png         
│
├── source/
│   ├── client/            
│   │   ├── app.js
│   │   ├── index.html
│   │   └── style.css
│   │
│   ├── server/              
│   │   ├── server.py
│   │   |   
│   │   └── turn_config.md   
│   │
│   └── scripts/             
│
└── README.md               

**⚙️ Cài đặt & chạy nhanh (Localhost / LAN)**
🔧 1. Cài Python và dependencies
cd source/server
pip install -r requirements.txt

▶️ 2. Chạy signaling server
python server.py


Server HTTP + WebSocket sẽ khởi động tại:
📍 http://localhost:8000 (HTTP)
📍 ws://localhost:8765 (WebSocket)

💻 3. Mở ứng dụng trên trình duyệt

Mở 2 tab trình duyệt tại địa chỉ:

http://localhost:8000


Nhập cùng Room ID ở cả hai tab.

Cho phép truy cập camera + microphone.

Hai tab sẽ thấy video của nhau và chat qua AES-DataChannel.

🌐 Demo trên nhiều máy (cùng mạng LAN)

Trên máy chạy server, lấy IP LAN (ví dụ: 172.11.59.61).

Trên máy khác cùng mạng, mở:

http://172.11.59.61:8000


WebSocket tự động dùng:

ws://172.11.59.61:8765


⚠️ Trên mobile Chrome, cần HTTPS để truy cập camera/mic.

Xem hướng dẫn trong source/server/README.md để chạy ngrok nhanh.

🌍 Xuyên NAT với TURN Server (coturn)

Dựng coturn theo hướng dẫn trong
source/server/turn_config.md

Cập nhật phần ICE servers trong:

source/client/app.js


🔐 Mã hóa AES-GCM động

Các gói tin từ DataChannel được mã hóa bằng AES-GCM 256-bit.

Hệ thống tự xoay khóa định kỳ để đảm bảo an toàn.

Việc mã hóa/giải mã được xử lý toàn bộ phía client (trong app.js).

**📦 Yêu cầu hệ thống**
Thành phần	Phiên bản khuyến nghị
Python	≥ 3.8
Node.js	≥ 18 (nếu build frontend)
Trình duyệt	Chrome / Edge / Firefox (>= 100)
Mạng	LAN hoặc NAT có STUN/TURN
🧩 Sơ đồ hệ thống
  [ Browser A ] ←→ [ WebSocket Server (Python) ] ←→ [ Browser B ]
         ↕                    ↑                          ↕
       WebRTC             Signaling                 WebRTC
         ↕                    ↓                          ↕
      STUN/TURN          NAT Traversal              STUN/TURN


Xem thêm file statics/diagram.png để biết chi tiết cấu trúc truyền thông.

**🧠 Tài liệu liên quan**

WebRTC Overview – MDN

DTLS/SRTP Security Architecture

TURN/STUN (coturn)

AES-GCM Spec – NIST

