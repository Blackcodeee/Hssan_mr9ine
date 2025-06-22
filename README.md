<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🔐 Hacker Access Only</title>
    <style>
        /* DARK HACKER THEME */
        body {
            background-color: #000;
            color: #0f0;
            font-family: 'Courier New', monospace;
            margin: 0;
            padding: 0;
            overflow: hidden;
        }

        .matrix-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            opacity: 0.3;
        }

        .login-container {
            background-color: rgba(0, 0, 0, 0.8);
            border: 2px solid #0f0;
            border-radius: 5px;
            width: 400px;
            margin: 100px auto;
            padding: 30px;
            box-shadow: 0 0 20px #0f0;
            text-align: center;
            animation: flicker 0.5s infinite alternate;
        }

        @keyframes flicker {
            0% { opacity: 0.9; }
            100% { opacity: 1; }
        }

        h1 {
            color: #0f0;
            text-shadow: 0 0 10px #0f0;
            margin-bottom: 30px;
        }

        input {
            background: #111;
            border: 1px solid #0f0;
            color: #0f0;
            padding: 10px;
            width: 80%;
            margin: 10px 0;
            font-family: 'Courier New', monospace;
        }

        button {
            background: #0f0;
            color: #000;
            border: none;
            padding: 10px 20px;
            margin-top: 20px;
            cursor: pointer;
            font-weight: bold;
            transition: 0.3s;
        }

        button:hover {
            background: #0a0;
            box-shadow: 0 0 10px #0f0;
        }

        .error {
            color: #f00;
            text-shadow: 0 0 5px #f00;
            animation: shake 0.5s;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            20%, 60% { transform: translateX(-5px); }
            40%, 80% { transform: translateX(5px); }
        }

        .success {
            color: #0f0;
            text-shadow: 0 0 10px #0f0;
            animation: pulse 1s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.7; }
            100% { opacity: 1; }
        }

        .hidden {
            display: none;
        }

        .secret-page {
            background-color: #000;
            color: #0f0;
            padding: 50px;
            text-align: center;
        }

        .secret-page h1 {
            font-size: 3em;
            margin-bottom: 30px;
        }

        .secret-page p {
            font-size: 1.5em;
        }
    </style>
</head>
<body>
    <!-- MATRIX BACKGROUND EFFECT -->
    <canvas class="matrix-bg" id="matrix"></canvas>

    <!-- LOGIN PAGE -->
    <div class="login-container" id="loginPage">
        <h1>🔒 SECURE SYSTEM ACCESS</h1>
        <p>ENTER PASSWORD TO CONTINUE</p>
        
        <input type="password" id="passwordInput" placeholder="Password..." autocomplete="off">
        <br>
        <button onclick="checkPassword()">LOGIN</button>
        
        <p id="errorMsg" class="hidden"></p>
    </div>

    <!-- SECRET PAGE (ONLY IF PASSWORD IS CORRECT) -->
    <div class="secret-page hidden" id="secretPage">
        <h1>WELCOME🤝</h1>
        <p> For more infomatiom STAY CONNECT</p>
        <p> <span id="secretData">Loading...</span></p>
    </div>

    <script>
        // MATRIX BACKGROUND ANIMATION
        const canvas = document.getElementById('matrix');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        
        const chars = "01";
        const fontSize = 14;
        const columns = canvas.width / fontSize;
        const drops = [];
        
        for (let i = 0; i < columns; i++) {
            drops[i] = 1;
        }
        
        function drawMatrix() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            ctx.fillStyle = '#0f0';
            ctx.font = fontSize + 'px monospace';
            
            for (let i = 0; i < drops.length; i++) {
                const text = chars.charAt(Math.floor(Math.random() * chars.length));
                ctx.fillText(text, i * fontSize, drops[i] * fontSize);
                
                if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
                    drops[i] = 0;
                }
                
                drops[i]++;
            }
        }
        
        setInterval(drawMatrix, 33);

        // PASSWORD CHECKER
        function checkPassword() {
            const password = document.getElementById('passwordInput').value;
            const errorMsg = document.getElementById('errorMsg');
            const loginPage = document.getElementById('loginPage');
            const secretPage = document.getElementById('secretPage');
            
            if (password === "Hassan") {
                // CORRECT PASSWORD
                errorMsg.classList.add('hidden');
                loginPage.classList.add('hidden');
                secretPage.classList.remove('hidden');
                
                // Simulate loading secret data
                setTimeout(() => {
                    document.getElementById('secretData').textContent = "Mr 9ine Database Accessed! ";
                }, 1500);
            } else {
                // WRONG PASSWORD
                errorMsg.textContent = "ACCESS DENIED! TRY AGAIN.";
                errorMsg.classList.remove('hidden');
                errorMsg.classList.add('error');
                
                // Reset animation
                setTimeout(() => {
                    errorMsg.classList.remove('error');
                }, 1000);
                
                // Clear input
                document.getElementById('passwordInput').value = "";
            }
        }
        
        // ENTER KEY TRIGGER
        document.getElementById('passwordInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                checkPassword();
            }
        });
    </script>
</body>
</html>
