# Fetch-API

# HTML


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>API Data Fetcher</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <div class="container">
        <h1>API Data Fetcher</h1>

        <button id="loadBtn">Load Users</button>

        <p id="message">Button par click karo.</p>

        <div id="users"></div>
    </div>

    <script src="script.js"></script>
</body>
</html>

# CSS


body {
    font-family: Arial, sans-serif;
    background: #f1f5f9;
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 800px;
    margin: 30px auto;
    text-align: center;
}

h1 {
    color: #1e293b;
}

button {
    background: #2563eb;
    color: white;
    border: none;
    padding: 12px 20px;
    border-radius: 6px;
    cursor: pointer;
}

button:hover {
    background: #1d4ed8;
}

#users {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 15px;
    margin-top: 20px;
}

.user-card {
    background: white;
    padding: 15px;
    border-radius: 8px;
    text-align: left;
    box-shadow: 0 2px 6px #00000015;
    overflow-wrap: anywhere;
}

#message {
    color: #475569;
}

# JS


const loadBtn = document.getElementById("loadBtn");
const usersDiv = document.getElementById("users");
const message = document.getElementById("message");

async function getUsers() {
    try {
        message.textContent = "Loading users...";
        usersDiv.innerHTML = "";

        const response = await fetch(
            "https://jsonplaceholder.typicode.com/users"
        );

        const users = await response.json();

        message.textContent = "Users successfully loaded!";

        users.forEach(function(user) {
            const card = document.createElement("div");

            card.className = "user-card";

            card.innerHTML = `
                <h3>${user.name}</h3>
                <p>Email: ${user.email}</p>
                <p>Phone: ${user.phone}</p>
            `;

            usersDiv.appendChild(card);
        });

    } catch (error) {
        message.textContent = "Error: Data load nahi hua.";
    }
}

loadBtn.addEventListener("click", getUsers);
