# 🧠 Live Collaborative Whiteboard (AI-Assisted)

A **real-time collaborative whiteboard application** built using **Java Spring Boot**, **WebSockets**, and **PostgreSQL**, where multiple users can draw simultaneously on a shared canvas.  
All drawing actions are synchronized in real time and persisted in the database.  
The project also demonstrates **AI-assisted development workflows** using tools like **Cursor / Anti-Gravity AI**.

---

## 🔗 Project Links

- **GitHub Repository:**  
  👉 https://github.com/YOUR_USERNAME/live-whiteboard

- **Live Deployed App (Render):**  
  👉 https://your-app-name.onrender.com

- **Database (Aiven – PostgreSQL):**  
  Hosted and managed PostgreSQL database

---

## ✨ Features

- 🎨 Real-time drawing on a shared canvas
- 👥 Multiple participants on the same board
- 🔄 Instant stroke synchronization using WebSockets
- 💾 Persistent storage of boards and strokes (PostgreSQL)
- 🔗 Join board via Board ID or URL
- ☁️ Deployed backend (Render)
- 🤖 AI-assisted development (Cursor / Anti-Gravity)

---

## 🏗️ High-Level Architecture


### Architecture Explanation (Simple)

- **Frontend**
  - HTML Canvas for drawing
  - JavaScript captures mouse/touch events
  - WebSocket connection for real-time sync

- **Backend (Spring Boot)**
  - REST APIs for board creation & loading
  - WebSocket server for live collaboration
  - JPA for database operations

- **Database**
  - PostgreSQL stores boards and strokes
  - Ensures drawings persist even after refresh or reconnect

---

## 🔌 WebSocket Flow (Real-Time Sync)

1. User opens a whiteboard in the browser
2. Browser establishes a **WebSocket connection**
3. When a user draws:
   - Stroke data (x, y, color, width) is sent to server
4. Server:
   - Saves the stroke in PostgreSQL
   - Broadcasts it to all connected users on the same board
5. Other users instantly see the drawing

### Why WebSockets?
- Low latency
- Bi-directional communication
- Perfect for real-time collaboration apps

---

## 🗄️ Database Design (PostgreSQL)

### 1️⃣ `whiteboards` table

| Column       | Type        | Description |
|-------------|-------------|-------------|
| id          | UUID (PK)   | Unique board ID |
| name        | VARCHAR     | Board name |
| created_at | TIMESTAMP   | Creation time |

### 2️⃣ `strokes` table

| Column       | Type        | Description |
|-------------|-------------|-------------|
| id          | UUID (PK)   | Stroke ID |
| board_id   | UUID (FK)   | Linked whiteboard |
| x           | FLOAT       | X coordinate |
| y           | FLOAT       | Y coordinate |
| color       | VARCHAR     | Stroke color |
| width       | INT         | Stroke width |
| created_at | TIMESTAMP   | Draw time |

### Database Planning Rationale

- **One board → many strokes**
- Normalized structure
- Easy to replay strokes when a user reconnects
- Scales well for multiple users and boards

---

## 📂 Project Structure Explained

