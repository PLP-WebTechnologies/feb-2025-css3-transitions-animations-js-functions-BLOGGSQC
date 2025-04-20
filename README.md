<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>User Preferences</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      transition: background-color 0.5s ease, color 0.5s ease;
      padding: 2rem;
      text-align: center;
    }

    .form-box {
      background: #fff;
      padding: 1.5rem;
      max-width: 400px;
      margin: auto;
      border-radius: 10px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }

    input, select, button {
      width: 100%;
      margin-top: 0.7rem;
      padding: 0.6rem;
      font-size: 1rem;
      border-radius: 6px;
      border: 1px solid #ccc;
    }

    button {
      background-color: #007bff;
      color: white;
      cursor: pointer;
      transition: background-color 0.4s ease;
    }

    button:hover {
      background-color: #0056b3;
    }

    #greeting {
      margin-top: 2rem;
      font-size: 1.5rem;
      opacity: 0;
      transform: scale(0.9);
    }

    /* CSS Animation */
    .fade-in {
      animation: fadeInScale 0.7s ease-out forwards;
    }

    @keyframes fadeInScale {
      from {
        opacity: 0;
        transform: scale(0.9);
      }
      to {
        opacity: 1;
        transform: scale(1);
      }
    }

    /* Dark theme class */
    .dark {
      background-color: #121212;
      color: #f1f1f1;
    }

    .dark .form-box {
      background: #1e1e1e;
      color: white;
    }

    .dark input, .dark select, .dark button {
      background-color: #2c2c2c;
      color: white;
      border: 1px solid #444;
    }
  </style>
</head>
<body>

  <h2>Customize Your Experience</h2>

  <div class="form-box">
    <label for="username">Your Name:</label>
    <input type="text" id="username" placeholder="Enter your name">

    <label for="theme">Choose Theme:</label>
    <select id="theme">
      <option value="light">Light</option>
      <option value="dark">Dark</option>
    </select>

    <button onclick="savePreferences()">Save Preferences</button>
  </div>

  <div id="greeting"></div>

  <script>
    // Load preferences if available
    window.addEventListener('DOMContentLoaded', () => {
      const savedName = localStorage.getItem('username');
      const savedTheme = localStorage.getItem('theme');

      if (savedName && savedTheme) {
        document.getElementById('username').value = savedName;
        document.getElementById('theme').value = savedTheme;
        applyTheme(savedTheme);
        showGreeting(savedName);
      }
    });

    // Save preferences and apply changes
    function savePreferences() {
      const name = document.getElementById('username').value.trim();
      const theme = document.getElementById('theme').value;

      if (!name) {
        alert("Please enter your name.");
        return;
      }

      // Store in localStorage
      localStorage.setItem('username', name);
      localStorage.setItem('theme', theme);

      // Apply theme + animation
      applyTheme(theme);
      showGreeting(name);
    }

    // Function to apply theme
    function applyTheme(theme) {
      document.body.classList.toggle('dark', theme === 'dark');
    }

    // Function to display greeting with animation
    function showGreeting(name) {
      const greeting = document.getElementById('greeting');
      greeting.textContent = `Hello, ${name}! 👋`;
      greeting.classList.remove('fade-in'); // Reset
      void greeting.offsetWidth; // Reflow
      greeting.classList.add('fade-in');
    }
  </script>
</body>
</html>
