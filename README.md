# 🗳️ Real-Time Polling App

A lightweight, real-time polling app where users can join a shared room, vote on one of two options (e.g., "Cats vs Dogs"), and see live results. Built using **React** for the frontend and **Node.js** with **WebSocket (Socket.IO)** on the backend.

---

## ✨ Features

### ✅ Frontend (ReactJS)
- Users can **enter a unique name** and either:
  - Create a new poll room
  - Join an existing room via a room code
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



---

## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/your-username/realtime-polling-app.git
cd realtime-polling-app

# Install server dependencies
cd server
npm install

# Install client dependencies
cd ../client
npm install

# Start backend
cd server
node index.js

# Start frontend
cd ../client
npm start

🧠 Vote State Sharing & Room Management
When a user joins a room:

Their socket joins via socket.join(roomCode)

Server stores room info in an in-memory object:
const rooms = {
  roomCode123: {
    question: 'Cats vs Dogs',
    votes: { user1: 'Cats', user2: 'Dogs' },
    timer: 60, // seconds
    hasEnded: false
  }
}
When voting:

The user's vote is stored

A voteUpdate event is emitted to all clients in the room

After 60 seconds:

The room is locked

A votingEnded event is broadcast to freeze UI and show results

📜 License
MIT License. ashajyothi

---

Would you like me to also generate a simple `index.js` for the Node.js WebSocket server or a basic React page for room creation and voting?
