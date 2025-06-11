# FreeIndia1
MUKESH KHICHAR (JAI SHREE RAM )

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FreeIndiaVerse</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            text-align: center;
        }
        .search-bar {
            width: 80%;
            padding: 10px;
            margin: 20px;
        }
        .category-filter {
            width: 80%;
            padding: 10px;
            margin: 20px;
        }
        .app-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
        }
        .app-card {
            border: 1px solid #ccc;
            padding: 10px;
            border-radius: 5px;
        }
        .app-card img {
            max-width: 100%;
        }
        .view-details-btn {
            background: #007bff;
            color: white;
            padding: 10px;
            text-decoration: none;
            border-radius: 5px;
            display: block;
            margin-top: 10px;
        }
        .download-btn {
            background: #28a745;
            color: white;
            padding: 10px;
            text-decoration: none;
            border-radius: 5px;
            display: block;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h1>Welcome to FreeIndiaVerse</h1>
    <select id="categoryFilter" class="category-filter">
        <option value="">All Categories</option>
        <option value="Games">Games</option>
        <option value="Tools">Tools</option>
        <option value="Education">Education</option>
        <option value="Productivity">Productivity</option>
        <option value="Entertainment">Entertainment</option>
        <option value="Other">Other</option>
    </select>
    <input type="text" class="search-bar" placeholder="Search Apps..." id="search">
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
        const db = firebase.firestore();

        // Load apps function
        function loadApps() {
            let category = document.getElementById('categoryFilter').value;
            let query = db.collection("apps");
            if (category) {
                query = query.where("category", "==", category);
            }
            query.get().then((querySnapshot) => {
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
                        <a href="app.html?id=${doc.id}" class="view-details-btn">View Details</a>
                        <a href="${app.apkUrl}" class="download-btn" download>Download APK</a>
                    `;
                    appGrid.appendChild(card);
                });
            });
        }

        // Initial load
        loadApps();

        // Category filter change
        document.getElementById('categoryFilter').addEventListener('change', loadApps);

        // Search functionality
        document.getElementById('search').addEventListener('input', (e) => {
            let query = e.target.value.toLowerCase();
            db.collection("apps").get().then((querySnapshot) => {
                let appGrid = document.getElementById('appGrid');
                appGrid.innerHTML = '';
                querySnapshot.forEach((doc) => {
                    let app = doc.data();
                    if (app.name.toLowerCase().includes(query) || app.description.toLowerCase().includes(query)) {
                        let card = document.createElement('div');
                        card.className = 'app-card';
                        card.innerHTML = `
                            <img src="${app.imageUrl}" alt="${app.name}">
                            <h3>${app.name}</h3>
                            <p>${app.description}</p>
                            <p>Category: ${app.category}</p>
                            <a href="app.html?id=${doc.id}" class="view-details-btn">View Details</a>
                            <a href="${app.apkUrl}" class="download-btn" download>Download APK</a>
                        `;
                        appGrid.appendChild(card);
                    }
                });
            });
        });
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Upload App - FreeIndiaVerse</title>
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
        input, textarea, select, button {
            margin: 10px;
            padding: 10px;
        }
    </style>
</head>
<body>
    <div id="authStatus"></div>
    <form id="uploadForm" style="display: none;">
        <input type="text" id="appName" placeholder="App Name" required>
        <textarea id="description" placeholder="Description" required></textarea>
        <select id="category" required>
            <option value="">Select Category</option>
            <option value="Games">Games</option>
            <option value="Tools">Tools</option>
            <option value="Education">Education</option>
            <option value="Productivity">Productivity</option>
            <option value="Entertainment">Entertainment</option>
            <option value="Other">Other</option>
        </select>
        <input type="file" id="apkFile" accept=".apk" required>
        <input type="file" id="appImage" accept="image/*" required>
        <button type="submit">Upload</button>
    </form>

    <!-- Firebase SDK -->
    <script src="[invalid url, do not cite]
    <script src="[invalid url, do not cite]
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
        const storage = firebase.storage();
        const db = firebase.firestore();
        const auth = firebase.auth();

        // Auth state change
        auth.onAuthStateChanged((user) => {
            if (user) {
                document.getElementById('uploadForm').style.display = 'block';
                document.getElementById('authStatus').innerHTML = `<p>Welcome, ${user.email} | <a href="#" id="logout">Logout</a></p>`;
                document.getElementById('logout').addEventListener('click', () => {
                    auth.signOut().then(() => {
                        window.location.href = "index.html";
                    });
                });
            } else {
                document.getElementById('uploadForm').style.display = 'none';
                document.getElementById('authStatus').innerHTML = '<p>Please <a href="login.html">login</a> to upload apps.</p>';
            }
        });

        // Upload form submission
        document.getElementById('uploadForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            const appName = document.getElementById('appName').value;
            const description = document.getElementById('description').value;
            const category = document.getElementById('category').value;
            const apkFile = document.getElementById('apkFile').files[0];
            const appImage = document.getElementById('appImage').files[0];

            // Upload APK to Firebase Storage
            const apkRef = storage.ref('apks/' + apkFile.name);
            await apkRef.put(apkFile);
            const apkUrl = await apkRef.getDownloadURL();

            // Upload Image to Firebase Storage
            const imgRef = storage.ref('images/' + appImage.name);
            await imgRef.put(appImage);
            const imgUrl = await imgRef.getDownloadURL();

            // Save app details to Firestore
            await db.collection('apps').add({
                name: appName,
                description: description,
                category: category,
                apkUrl: apkUrl,
                imageUrl: imgUrl,
                timestamp: firebase.firestore.FieldValue.serverTimestamp()
            });

            alert('App uploaded successfully!');
            document.getElementById('uploadForm').reset();
        });
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>App Details - FreeIndiaVerse</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            text-align: center;
        }
        .app-details {
            max-width: 600px;
            margin: auto;
            text-align: left;
        }
        .download-btn {
            background: #28a745;
            color: white;
            padding: 10px;
            text-decoration: none;
            border-radius: 5px;
            display: inline-block;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h1>App Details</h1>
    <div class="app-details" id="appDetails">
        <!-- App details will be loaded here -->
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
        const db = firebase.firestore();

        // Get app ID from URL
        const urlParams = new URLSearchParams(window.location.search);
        const appId = urlParams.get('id');

        if (appId) {
            db.collection("apps").doc(appId).get().then((doc) => {
                if (doc.exists) {
                    let app = doc.data();
                    let appDetails = document.getElementById('appDetails');
                    appDetails.innerHTML = `
                        <h2>${app.name}</h2>
                        <img src="${app.imageUrl}" alt="${app.name}" style="max-width: 100%;">
                        <p>${app.description}</p>
                        <p>Category: ${app.category}</p>
                        <a href="${app.apkUrl}" class="download-btn" download>Download APK</a>
                    `;
                } else {
                    alert("App not found");
                }
            });
        } else {
            alert("No app ID provided");
        }
    </script>
</body>
</html>
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
    <h1>Login</h1>
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
                    alert("Logged in successfully");
                    window.location.href = "upload.html";
                })
                .catch((error) => {
                    alert(error.message);
                });
        });
    </script>
</body>
</html>
<!DOCTYPE html>
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
    <h1>Register</h1>
    <form id="registerForm">
        <input type="email" id="email" placeholder="Email" required>
        <input type="password" id="password" placeholder="Password" required>
        <button type="submit">Register</button>
    </form>
    <p>Already have an account? <a href="login.html">Login</a></p>

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
                    alert("Registered successfully");
                    window.location.href = "login.html";
                })
                .catch((error) => {
                    alert(error.message);
                });
        });
    </script>
</body>
</html>
