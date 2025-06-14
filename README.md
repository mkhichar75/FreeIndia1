# FreeIndia1
MUKESH KHIHAR (JAI SHREE RAM )
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login - FreeIndiaVerse</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            text-align: center;
        }
        form {
            display: flex;
            flex-direction: column;
            width: 300px;
            margin: auto;
        }
        input, button {
            margin: 10px;
            padding: 10px;
        }
    </style>
</head>
<body>
    <h1>Login to FreeIndiaVerse</h1>
    <form id="loginForm">
        <input type="email" id="email" placeholder="Email" required>
        <input type="password" id="password" placeholder="Password" required>
        <button type="submit">Login</button>
    </form>
    <p>Don't have an account? <a href="register.html">Register</a></p>

    <!-- Firebase SDK -->
    <script src="[invalid url, do not cite]
    <script src="[invalid url, do not cite]
    <script>
        // Firebase configuration
        const firebaseConfig = {
            apiKey: "YOUR_API_KEY",
            authDomain: "YOUR_AUTH_DOMAIN",
            projectId: "YOUR_PROJECT_ID",
            storageBucket: "YOUR_STORAGE_BUCKET",
            messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
            appId: "YOUR_APP_ID"
        };
        firebase.initializeApp(firebaseConfig);
        const auth = firebase.auth();

        document.getElementById('loginForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;
            auth.signInWithEmailAndPassword(email, password)
                .then((userCredential) => {
                    // Signed in
                    window.location.href = "profile.html";
                })
                .catch((error) => {
                    alert(error.message);
                });
        });
    </script>
</body>
</html><!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Register - FreeIndiaVerse</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            text-align: center;
        }
        form {
            display: flex;
            flex-direction: column;
            width: 300px;
            margin: auto;
        }
        input, button {
            margin: 10px;
            padding: 10px;
        }
    </style>
</head>
<body>
    <h1>Register for FreeIndiaVerse</h1>
    <form id="registerForm">
        <input type="email" id="email" placeholder="Email" required>
        <input type="password" id="password" placeholder="Password" required>
        <button type="submit">Register</button>
    </form>
    <p>Already have an account? <a href="index.html">Login</a></p>

    <!-- Firebase SDK -->
    <script src="[invalid url, do not cite]
    <script src="[invalid url, do not cite]
    <script>
        // Firebase configuration
        const firebaseConfig = {
            apiKey: "YOUR_API_KEY",
            authDomain: "YOUR_AUTH_DOMAIN",
            projectId: "YOUR_PROJECT_ID",
            storageBucket: "YOUR_STORAGE_BUCKET",
            messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
            appId: "YOUR_APP_ID"
        };
        firebase.initializeApp(firebaseConfig);
        const auth = firebase.auth();

        document.getElementById('registerForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;
            auth.createUserWithEmailAndPassword(email, password)
                .then((userCredential) => {
                    // Registered
                    window.location.href = "index.html";
                })
                .catch((error) => {
                    alert(error.message);
                });
        });
    </script>
</body>
</html><!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Profile - FreeIndiaVerse</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            text-align: center;
        }
        form {
            display: flex;
            flex-direction: column;
            width: 300px;
            margin: auto;
        }
        input, button {
            margin: 10px;
            padding: 10px;
        }
        .heart {
            font-size: 50px;
            color: red;
            animation: blink 1s step-end infinite;
        }
        @keyframes blink {
            50% {
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <h1>Complete Your Profile</h1>
    <form id="profileForm">
        <input type="text" id="firstName" placeholder="First Name" required>
        <input type="text" id="lastName" placeholder="Last Name" required>
        <input type="text" id="country" placeholder="Country" required>
        <input type="text" id="state" placeholder="State" required>
        <button type="submit">Save</button>
    </form>
    <div style="margin-top: 20px;">
        <span class="heart" onclick="highlightHeart()">🩵</span>
    </div>

    <!-- Firebase SDK -->
    <script src="[invalid url, do not cite]
    <script src="[invalid url, do not cite]
    <script>
        // Firebase configuration
        const firebaseConfig = {
            apiKey: "YOUR_API_KEY",
            authDomain: "YOUR_AUTH_DOMAIN",
            projectId: "YOUR_PROJECT_ID",
            storageBucket: "YOUR_STORAGE_BUCKET",
            messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
            appId: "YOUR_APP_ID"
        };
        firebase.initializeApp(firebaseConfig);
        const auth = firebase.auth();
        const db = firebase.firestore();

        // Check if user is logged in
        auth.onAuthStateChanged((user) => {
            if (!user) {
                window.location.href = "index.html";
            } else {
                // Load profile if exists
                db.collection("users").doc(user.uid).get().then((doc) => {
                    if (doc.exists) {
                        const data = doc.data();
                        document.getElementById('firstName').value = data.firstName || '';
                        document.getElementById('lastName').value = data.lastName || '';
                        document.getElementById('country').value = data.country || '';
                        document.getElementById('state').value = data.state || '';
                    }
                });
            }
        });

        // Save profile
        document.getElementById('profileForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const user = auth.currentUser;
            if (user) {
                db.collection("users").doc(user.uid).set({
                    firstName: document.getElementById('firstName').value,
                    lastName: document.getElementById('lastName').value,
                    country: document.getElementById('country').value,
                    state: document.getElementById('state').value,
                    timestamp: firebase.firestore.FieldValue.serverTimestamp()
                }).then(() => {
                    window.location.href = "home.html";
                });
            }
        });

        // Highlight heart on click
        function highlightHeart() {
            const heart = document.querySelector('.heart');
            heart.style.color = 'red';
            heart.style.animation = 'none';
            setTimeout(() => {
                heart.style.animation = 'blink 1s step-end infinite';
            }, 1000);
        }
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FreeIndiaVerse - Home</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            text-align: center;
        }
        .sidebar {
            position: fixed;
            top: 20px;
            left: 20px;
            cursor: pointer;
        }
        .sidebar-content {
            display: none;
            position: absolute;
            background-color: #f9f9f9;
            min-width: 160px;
            box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
            z-index: 1;
        }
        .sidebar-content a {
            color: black;
            padding: 12px 16px;
            text-decoration: none;
            display: block;
        }
        .sidebar-content a:hover {
            background-color: #f1f1f1;
        }
        .show {
            display: block;
        }
        .options {
            margin-top: 50px;
        }
        .option-btn {
            background: #007bff;
            color: white;
            padding: 10px 20px;
            text-decoration: none;
            border-radius: 5px;
            display: inline-block;
            margin: 10px;
        }
        .app-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 50px;
        }
        .app-card {
            border: 1px solid #ccc;
            padding: 10px;
            border-radius: 5px;
        }
        .app-card img {
            max-width: 100%;
        }
    </style>
</head>
<body>
    <div class="sidebar" onclick="toggleSidebar()">
        ☰
    </div>
    <div class="sidebar-content" id="sidebarContent">
        <a href="profile.html">User Details</a>
        <a href="#">Settings</a>
        <a href="#">Suggest Ideas</a>
        <a href="#">Rating</a>
    </div>
    <h1>Welcome to FreeIndiaVerse</h1>
    <div class="options">
        <a href="upload.html" class="option-btn">Upload App</a>
        <a href="#" class="option-btn">Download Apps</a>
    </div>
    <div class="app-grid" id="appGrid">
        <!-- Apps will be dynamically added here -->
    </div>

    <!-- Firebase SDK -->
    <script src="[invalid url, do not cite]
    <script src="[invalid url, do not cite]
    <script>
        // Firebase configuration
        const firebaseConfig = {
            apiKey: "YOUR_API_KEY",
            authDomain: "YOUR_AUTH_DOMAIN",
            projectId: "YOUR_PROJECT_ID",
            storageBucket: "YOUR_STORAGE_BUCKET",
            messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
            appId: "YOUR_APP_ID"
        };
        firebase.initializeApp(firebaseConfig);
        const auth = firebase.auth();
        const db = firebase.firestore();

        // Check if user is logged in
        auth.onAuthStateChanged((user) => {
            if (!user) {
                window.location.href = "index.html";
            } else {
                // Load apps
                loadApps();
            }
        });

        // Sidebar toggle
        function toggleSidebar() {
            var sidebarContent = document.getElementById("sidebarContent");
            sidebarContent.classList.toggle("show");
        }

        // Load apps function
        function loadApps() {
            db.collection("apps").get().then((querySnapshot) => {
                let appGrid = document.getElementById('appGrid');
                appGrid.innerHTML = '';
                querySnapshot.forEach((doc) => {
                    let app = doc.data();
                    let card = document.createElement('div');
                    card.className = 'app-card';
                    card.innerHTML = `
                        <img src="${app.imageUrl}" alt="${app.name}">
                        <h3>${app.name}</h3>
                        <p>${app.description}</p>
                        <p>Category: ${app.category}</p>
                        <a href="app.html?id=${doc.id}">View Details</a>
                        <a href="${app.apkUrl}" download>Download APK</a>
                    `;
                    appGrid.appendChild(card);
                });
            });
        }
    </script>
</body>
</html>


# FreeIndia
mukesh/
├── public/
│   ├── index.html
│   ├── styles.css
│   ├── script.js
├── server.js
├── package.json
const express = require('express');
const mongoose = require('mongoose');
const multer = require('multer');
const { WebSocketServer } = require('ws');
const path = require('path');

const app = express();
const port = 3000;

// MongoDB setup
mongoose.connect('mongodb://localhost/mukesh', { useNewUrlParser: true, useUnifiedTopology: true });
const PostSchema = new mongoose.Schema({
  type: String, // 'video' or 'text'
  content: String,
  creator: Boolean,
  createdAt: { type: Date, default: Date.now }
});
const Post = mongoose.model('Post', PostSchema);

// Middleware
app.use(express.static('public'));
app.use(express.json());

// Video upload setup (10-minute limit, ~100MB max size)
const storage = multer.diskStorage({
  destination: 'public/uploads/',
  filename: (req, file, cb) => cb(null, Date.now() + path.extname(file.originalname))
});
const upload = multer({
  storage,
  limits: { fileSize: 100 * 1024 * 1024 } // 100MB
});

// Routes
app.get('/posts', async (req, res) => {
  const posts = await Post.find().sort({ createdAt: -1 });
  res.json(posts);
});

app.post('/upload', upload.single('video'), async (req, res) => {
  // Only creator can upload (simplified check, add auth in production)
  if (!req.body.isCreator) return res.status(403).json({ error: 'Unauthorized' });
  const post = new Post({
    type: 'video',
    content: `/uploads/${req.file.filename}`,
    creator: true
  });
  await post.save();
  res.json({ message: 'Video uploaded' });
});

app.post('/text-post', async (req, res) => {
  const { content } = req.body;
  if (!content || content.length > 280) return res.status(400).json({ error: 'Invalid post' });
  
  // Simple AI for humorous reply
  const aiResponses = [
    'Haha, nice one! 😎',
    'Bro, is this your stand-up debut? 😂',
    'Mukesh bhai, yeh toh viral hone wala hai! 🚀'
  ];
  const aiReply = aiResponses[Math.floor(Math.random() * aiResponses.length)];
  
  const post = new Post({
    type: 'text',
    content,
    creator: false
  });
  await post.save();
  res.json({ message: 'Post created', aiReply });
});

// WebSocket for group chat
const wss = new WebSocketServer({ port: 8080 });
wss.on('connection', ws => {
  ws.on('message', message => {
    wss.clients.forEach(client => {
      if (client.readyState === ws.OPEN) client.send(message.toString());
    });
  });
});

app.listen(port, () => console.log(`Server running on http://localhost:${port}`));
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mukesh.com</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="container">
    <!-- Header with Logo -->
    <header class="text-center my-3">
      <img src="logo.png" alt="Bangol Tiger Logo" class="logo">
      <h1>Mukesh.com</h1>
    </header>

    <!-- Video Upload (Creator Only) -->
    <div id="upload-section" class="mb-4">
      <h3>Upload Video (Creator)</h3>
      <input type="file" id="videoInput" accept="video/*">
      <button onclick="uploadVideo()" class="btn btn-primary">Upload</button>
    </div>

    <!-- Text Post -->
    <div id="post-section" class="mb-4">
      <h3>Post Something</h3>
      <textarea id="textPost" class="form-control" rows="3" maxlength="280"></textarea>
      <button onclick="submitPost()" class="btn btn-primary mt-2">Post</button>
      <div id="aiResponse" class="mt-2"></div>
    </div>

    <!-- Group Chat -->
    <div id="chat-section" class="mb-4">
      <h3>Group Chat</h3>
      <div id="chatBox" class="border p-3" style="height: 200px; overflow-y: scroll;"></div>
      <input type="text" id="chatInput" class="form-control mt-2" placeholder="Type a message...">
      <button onclick="sendMessage()" class="btn btn-primary mt-2">Send</button>
    </div>

    <!-- Homepage Posts -->
    <div id="posts" class="row"></div>

    <!-- Settings (Instagram Style) -->
    <div id="settings" class="mt-4">
      <h3>Settings</h3>
      <ul class="list-group">
        <li class="list-group-item">Profile</li>
        <li class="list-group-item">Privacy</li>
        <li class="list-group-item">Notifications</li>
      </ul>
    </div>
  </div>

  <script src="script.js"></script>
</body>
</html>
body {
  background-color: #fafafa;
  font-family: Arial, sans-serif;
}
.logo {
  width: 100px;
  height: auto;
}
#posts .post {
  background: white;
  border: 1px solid #dbdbdb;
  border-radius: 8px;
  padding: 10px;
  margin-bottom: 15px;
}
video {
  max-width: 100%;
  height: auto;
}
#chatBox {
  background: #fff;
  border: 1px solid #dbdbdb;
}
// Load posts on page load
window.onload = async () => {
  const response = await fetch('/posts');
  const posts = await response.json();
  const postsDiv = document.getElementById('posts');
  posts.forEach(post => {
    const div = document.createElement('div');
    div.className = 'col-md-4 post';
    if (post.type === 'video') {
      div.innerHTML = `<video controls src="${post.content}"></video>`;
    } else {
      div.innerHTML = `<p>${post.content}</p>`;
    }
    postsDiv.appendChild(div);
  });
};

// Video upload
async function uploadVideo() {
  const videoInput = document.getElementById('videoInput');
  const file = videoInput.files[0];
  if (!file) return alert('Select a video');
  const formData = new FormData();
  formData.append('video', file);
  formData.append('isCreator', true); // Simplified, add auth in production
  const response = await fetch('/upload', {
    method: 'POST',
    body: formData
  });
  const result = await response.json();
  alert(result.message);
  location.reload();
}

// Text post
async function submitPost() {
  const content = document.getElementById('textPost').value;
  if (!content) return alert('Write something');
  const response = await fetch('/text-post', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ content })
  });
  const result = await response.json();
  document.getElementById('aiResponse').innerText = result.aiReply;
  document.getElementById('textPost').value = '';
  location.reload();
}

// Group chat WebSocket
const ws = new WebSocket('ws://localhost:8080');
ws.onmessage = event => {
  const chatBox = document.getElementById('chatBox');
  const message = document.createElement('p');
  message.innerText = event.data;
  chatBox.appendChild(message);
  chatBox.scrollTop = chatBox.scrollHeight;
};

function sendMessage() {
  const input = document.getElementById('chatInput');
  if (input.value) {
    ws.send(input.value);
    input.value = '';
  }
}
mkdir mukesh
cd mukesh
npm init -y
npm install express mongoose multer ws
mkdir public public/uploads
node server.js
{
  "name": "Mukesh.com",
  "short_name": "Mukesh",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#fafafa",
  "theme_color": "#000000",
  "icons": [
    {
      "src": "/logo.png",
      "sizes": "192x192",
      "type": "image/png"
    }
  ]
}
const express = require('express');
const mongoose = require('mongoose');
const app = express();
const port = 3000;

// MongoDB setup
mongoose.connect('mongodb://localhost/mukesh', { useNewUrlParser: true, useUnifiedTopology: true });
const PostSchema = new mongoose.Schema({
  type: String,
  content: String,
  createdAt: { type: Date, default: Date.now }
});
const Post = mongoose.model('Post', PostSchema);

app.use(express.json());

// Text post endpoint
app.post('/text-post', async (req, res) => {
  const { content } = req.body;
  if (!content || content.length > 280) {
    return res.status(400).json({ error: 'Post must be 1-280 characters' });
  }

  // Simple AI for humorous reply
  const aiResponses = [
    'Haha, Mukesh bhai, yeh toh dil se dil tak jata hai! 😎',
    'Arre, yeh post toh viral hone wala hai! 😂',
    'Bohot badhiya, keep rocking! 🚀'
  ];
  const aiReply = aiResponses[Math.floor(Math.random() * aiResponses.length)];

  const post = new Post({
    type: 'text',
    content
  });
  await post.save();
  res.json({ message: 'Post created', aiReply });
});

app.listen(port, () => console.log(`Server running on http://localhost:${port}`));
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mukesh.com</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  <style>
    body { background-color: #fafafa; font-family: Arial, sans-serif; }
    .post { background: white; border: 1px solid #dbdbdb; border-radius: 8px; padding: 10px; margin-bottom: 15px; }
  </style>
</head>
<body>
  <div class="container">
    <!-- Text Post Section -->
    <div id="post-section" class="mb-4">
      <h3>Post Something</h3>
      <textarea id="textPost" class="form-control" rows="3" maxlength="280" placeholder="What's on your mind?"></textarea>
      <button onclick="submitPost()" class="btn btn-primary mt-2">Post</button>
      <div id="aiResponse" class="mt-2 text-success"></div>
    </div>

    <!-- Display Posts -->
    <div id="posts" class="row"></div>
  </div>

  <script src="script.js"></script>
</body>
</html>
// Load posts on page load
window.onload = async () => {
  const response = await fetch('/posts');
  const posts = await response.json();
  const postsDiv = document.getElementById('posts');
  posts.forEach(post => {
    if (post.type === 'text') {
      const div = document.createElement('div');
      div.className = 'col-md-4 post';
      div.innerHTML = `<p>${post.content}</p>`;
      postsDiv.appendChild(div);
    }
  });
};

// Submit text post
async function submitPost() {
  const content = document.getElementById('textPost').value;
  if (!content) return alert('Write something');
  const response = await fetch('/text-post', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ content })
  });
  const result = await response.json();
  if (result.error) {
    alert(result.error);
  } else {
    document.getElementById('aiResponse').innerText = `AI Reply: ${result.aiReply}`;
    document.getElementById('textPost').value = '';
    location.reload(); // Reload to show new post
  }
}
mkdir mukesh
cd mukesh
npm init -y
npm install express mongoose

mukesh/
├── public/
│   ├── index.html
│   ├── script.js
├── server.js
├── package.json
node server.js
