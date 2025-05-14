# 🗳️ Real‑Time Voting App

A lightweight, real-time polling app where users can join a shared room, vote on one of two options (e.g., "Cats vs Dogs"), and see live results. Built using **React** for the frontend and **Node.js** with **WebSocket (Socket.IO)** on the backend.

---

## ✨ Features

### ✅ Frontend (ReactJS)
- Users can **enter a unique name** and either:
  - **Create a new poll room**, or
  - **Join an existing room** via a room code
- Displays a simple **poll question with two options**
- Allows voting for **one option only**; disables further votes after submission
- **Real-time vote updates** across all clients using WebSocket
- Shows **which option the user voted for** (persisted via localStorage)
- **Voting closes after 60 seconds** with a visible countdown timer

### ✅ Backend (Node.js + Socket.IO)
- Supports **creation and storage** of poll rooms (in-memory)
- **Manages user connections**, disconnections, and room participation
- Handles **real-time vote broadcasting**
- Ensures **unique usernames per room**
- Automatically ends voting in a room after 60 seconds

---

## 📁 Project Structure

```plaintext
.
├── client/                 # React front‑end
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   └── App.jsx
│   └── package.json
├── server/                # Node.js backend
│   ├── index.js           # Express + Socket.io server
│   └── package.json
└── README.md
---
🚀 Getting Started
---
1️⃣ Clone the Repository
git clone https://github.com/your-username/realtime-polling-app.git
cd realtime-polling-app
---
2️⃣ Install Dependencies
# Backend
cd server
npm install

# Frontend
cd ../client
npm install
---
3️⃣ Run the App
# Start backend (from /server)
cd ../server
node index.js
---
# Start frontend (from /client)
cd ../client
npm start
---
 Vote State Sharing & Room Management
 When a user joins a room:
---
Their socket connects via:

socket.join(roomCode);
---

The server maintains in-memory room state:

const rooms = {
  "roomABC": {
    question: "Cats vs Dogs",
    votes: { "user1": "Cats", "user2": "Dogs" },
    timer: 60,
    hasEnded: false
  }
};

On vote submission:

User's vote is stored in the votes object

Server emits a voteUpdate event to all clients in the room

After 60 seconds:

hasEnded is set to true

A votingEnded event is sent to all clients to lock the UI and show final results
