<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bankysnoop</title>
    <style>
        /* General Styles */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f5f7fa;
            color: #333;
        }

        header {
            text-align: center;
            margin-bottom: 20px;
        }

        header h1 {
            color: #1652f0;
            font-size: 2.5rem;
        }

        header p {
            font-size: 1.2rem;
            color: #666;
        }

        .auth, .dashboard, .send-money {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
            max-width: 400px;
            margin-left: auto;
            margin-right: auto;
        }

        h2 {
            color: #1652f0;
            margin-bottom: 15px;
        }

        form {
            display: flex;
            flex-direction: column;
        }

        label {
            margin-bottom: 5px;
            font-weight: bold;
        }

        input {
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }

        button {
            padding: 10px;
            background-color: #1652f0;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

        button:hover {
            background-color: #1346d0;
        }

        #loginStatus, #transactionStatus {
            margin-top: 15px;
            font-weight: bold;
        }

        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <h1>Bankysnoop</h1>
        <p>Your Secure Crypto Banking Platform</p>
    </header>

    <!-- User Authentication Section -->
    <section class="auth">
        <h2>Login</h2>
        <form id="loginForm">
            <label for="username">Username:</label>
            <input type="text" id="username" required>
            <label for="password">Password:</label>
            <input type="password" id="password" required>
            <button type="submit">Login</button>
        </form>
        <p id="loginStatus"></p>
    </section>

    <!-- Dashboard Section (Hidden by Default) -->
    <section class="dashboard hidden">
        <h2>Your Dashboard</h2>
        <p>Welcome, <span id="loggedInUser"></span>!</p>
        <p>Balance: <span id="balance">12,000,000</span> USD</p>
    </section>

    <!-- Send Money Form (Hidden by Default) -->
    <section class="send-money hidden">
        <h2>Send Money</h2>
        <form id="sendForm">
            <label for="amount">Amount (USD):</label>
            <input type="number" id="amount" required>
            <label for="recipient">Recipient Address:</label>
            <input type="text" id="recipient" required>
            <button type="submit">Send</button>
        </form>
        <p id="transactionStatus"></p>
    </section>

    <script>
        // Mock User Credentials
        const mockUsername = "user123";
        const mockPassword = "password123";

        // Get Elements
        const loginForm = document.getElementById('loginForm');
        const loginStatus = document.getElementById('loginStatus');
        const dashboardSection = document.querySelector('.dashboard');
        const sendMoneySection = document.querySelector('.send-money');
        const loggedInUser = document.getElementById('loggedInUser');
        const balanceElement = document.getElementById('balance');
        const sendForm = document.getElementById('sendForm');
        const transactionStatus = document.getElementById('transactionStatus');

        // Initial Balance
        let balance = 12000000;

        // Handle Login Form Submission
        loginForm.addEventListener('submit', (e) => {
            e.preventDefault(); // Prevent page reload

            // Get form values
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;

            // Validate credentials
            if (username === mockUsername && password === mockPassword) {
                loginStatus.textContent = "Login successful!";
                loginStatus.style.color = "green";

                // Show dashboard and send money sections
                dashboardSection.classList.remove('hidden');
                sendMoneySection.classList.remove('hidden');
                loginForm.classList.add('hidden');

                // Display logged-in user
                loggedInUser.textContent = username;
            } else {
                loginStatus.textContent = "Invalid username or password.";
                loginStatus.style.color = "red";
            }
        });

        // Handle Send Money Form Submission
        sendForm.addEventListener('submit', (e) => {
            e.preventDefault(); // Prevent page reload

            // Get form values
            const amount = parseFloat(document.getElementById('amount').value);
            const recipient = document.getElementById('recipient').