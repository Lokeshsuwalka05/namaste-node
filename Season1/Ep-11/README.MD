# 🌐 Server, Networking & Node.js Event Loop

## 🔹 What is a Server?

- A **server** is like a computer that has its own OS and runs different applications inside it.
- A server always **waits for a request** (via sockets or HTTP), and once a request comes, it responds with data (file, text, JSON, image, etc.).
- Example: Think about **AWS servers**. They are basically a hub of powerful computing machines where millions of clients make requests and get responses. AWS has huge data centers to handle all this.

---

## 🔹 Why not use our own computer as a server?

Technically, your computer **can act as a server**. But it has limitations:

- Limited **RAM** and **CPU power** (cannot handle thousands/millions of requests).
- Limited **network bandwidth** (your home Wi-Fi cannot serve millions of users).
- **No global availability** — your PC can’t be accessed everywhere easily.
- **Reliability issues** — your system may crash, shut down, or overheat.
- **Security risks** — personal machines aren’t hardened like cloud servers.

👉 That’s why companies prefer cloud providers like **AWS, GCP, Azure** — they offer scalability, reliability, and global access.

---

## 🔹 Types of Servers

- **HTTP Server** → For websites & APIs (most common).
- **SMTP Server** → For emails.
- **FTP Server** → For file transfers.
- **Database Server** → For storing/querying data.

👉 But when we talk about **Web Servers**, we mostly mean **HTTP servers**.

---

## 🔹 How does Client–Server Communication Work?

The rules of communication are defined by **TCP/IP model** (practical) and **OSI model** (theoretical reference).

### ✅ Correct Flow of Data (when sending):

1. **Application Layer** → Data is created (e.g., WhatsApp message, photo).  
   👉 “Data aaya Application Layer pe.”

2. **Transport Layer (TCP/UDP)** → Breaks the data into **segments**, adds **port numbers** and ensures reliability (TCP).  
   👉 “Data ko toda Transmission Layer ne.”

3. **Internet Layer (IP)** → Each segment gets a **source & destination IP address**, forming a **packet**.  
   👉 “Chunks ko IP diya Internet Layer ne.”

4. **Network Access Layer (Link Layer)** → Adds **MAC address** and defines the medium (Wi-Fi, Ethernet, 4G). Packets become **frames**.  
   👉 “Medium define kiya Network Layer ne.”

📩 On the **server side**, the process happens in reverse:  
`Network Access → Internet → Transport → Application`

---

## 🔹 Example: When You Open `namastedev.com`

1. Your request first goes to a **DNS server**.
2. DNS resolves the domain name into an **IP address**.
3. With that IP, your browser sends an **HTTP request** to the server.
4. The server processes it and sends back the response (HTML/JSON/etc.).

---

## 🔹 Can I create multiple HTTP servers?

✅ Yes! You can create as many as you want.  
But how do we differentiate them?

- By **Port Numbers**.
- So the combination of `(IP + Port)` uniquely identifies a server.

Example:

- `127.0.0.1:3000` → First HTTP server
- `127.0.0.1:4000` → Second HTTP server

---

## 🔹 Socket vs WebSocket

### 🔸 Normal Socket (TCP Socket)

- A **socket** = `(IP + Port)` = endpoint of communication.
- With **TCP sockets**:
  - Client connects to server.
  - Data is exchanged.
  - Connection may be **closed** or kept alive (depends on protocol).

Example:  
HTTP uses TCP socket on port 80/443.

- Client sends request → Server sends response → Connection usually closes (unless **keep-alive** is enabled).

---

### 🔸 WebSocket

- WebSocket is built **on top of TCP sockets**.
- Starts as an **HTTP handshake**, then “upgrades” to WebSocket.
- Connection stays **open & persistent** (full-duplex).
- Both client & server can send messages anytime (without reconnecting).

Used for **real-time apps** like:

- WhatsApp Web
- Stock tickers
- Multiplayer games
- Live chat / Notifications

---

## 🔹 Node.js Event Loop Phases

The **event loop** handles asynchronous operations in Node.js. It has multiple phases:

1. **Timers Phase**  
   Executes callbacks from `setTimeout()` and `setInterval()`.

2. **Pending Callbacks Phase**  
   Executes I/O callbacks that were deferred (e.g., TCP errors).

3. **Idle, Prepare Phase**  
   Internal use only.

4. **Poll Phase**

   - Retrieves new I/O events.
   - Executes I/O callbacks (like `fs.readFile`).
   - If no timers are waiting, it will block here for new events.

5. **Check Phase**  
   Executes `setImmediate()` callbacks.

6. **Close Callbacks Phase**  
   Executes close event callbacks (e.g., `socket.on('close', ...)`).

---

## 🔹 Creating Servers in Node.js

- We can create servers using Node.js by using the **http module**, but it can become complicated for large apps.
- That’s why we use **Express.js**, which is built on top of Node.js, and makes server creation easier.

---

## 🔹 Different Meanings of the Word “Server”

1. **Hardware Server**

   - A physical computer machine designed to serve many clients.
   - Has more RAM, CPU cores, storage, and high network capacity.
   - Example: Dell, HP, IBM machines in data centers.
   - **Purpose**: Handle multiple client requests.

2. **Software Server**

   - A program/application that acts as a server.
   - Examples:
     - Apache / Nginx → Web servers
     - MySQL / PostgreSQL → Database servers
     - Node.js `http` module
   - **Purpose**: Accept requests and send responses.

3. **Application Server**
   - A server designed to run applications for specific purposes.
   - Examples:
     - Tomcat → Runs Java apps
     - Express.js app → Runs Node.js applications
     - Spring Boot → Runs enterprise Java apps

---

✅ This covers: **Server basics, TCP/IP communication, multiple servers, sockets vs WebSockets, Node.js event loop, and types of servers (hardware/software/application).**
