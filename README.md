<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Shared Life Update</title>
  <script type="module">
    // Import the functions you need from the SDKs you need
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.2.0/firebase-app.js";
    import { getFirestore, collection, addDoc, getDocs } from "https://www.gstatic.com/firebasejs/11.2.0/firebase-firestore.js";

    // Your web app's Firebase configuration
    const firebaseConfig = {
      apiKey: "AIzaSyDC7B7hH8DzaICObYeThitZGjB1T6kOxuE",
      authDomain: "samgupdates.firebaseapp.com",
      projectId: "samgupdates",
      storageBucket: "samgupdates.firebasestorage.app",
      messagingSenderId: "478785184923",
      appId: "1:478785184923:web:f1658991490e1bd8e2523e"
    };

    // Initialize Firebase
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    // Fetch and render messages
    async function fetchMessages() {
      const messagesSnapshot = await getDocs(collection(db, "messages"));
      const messages = messagesSnapshot.docs.map(doc => doc.data());

      const messagesDiv = document.getElementById('messages');
      messagesDiv.innerHTML = messages
        .map(message => `
          <div class="message">
            <p><strong>${message.name}</strong></p>
            <p>${message.text}</p>
            <p class="meta">${message.date}</p>
          </div>
        `)
        .join('');
    }

    // Handle form submission
    async function handleFormSubmit(event) {
      event.preventDefault();

      const name = document.getElementById('name').value.trim();
      const text = document.getElementById('message').value.trim();
      const date = new Date().toLocaleString();

      // Add message to Firestore
      await addDoc(collection(db, "messages"), { name, text, date });

      // Clear form
      document.getElementById('name').value = '';
      document.getElementById('message').value = '';

      // Fetch and render updated messages
      fetchMessages();
    }

    // Initialize form submission listener and fetch messages on load
    window.onload = () => {
      document.getElementById('messageForm').addEventListener('submit', handleFormSubmit);
      fetchMessages();
    };
  </script>
  <style>
    /* Add your CSS styling here */
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      margin: 0;
      padding: 0;
    }
    .container {
      max-width: 600px;
      margin: 2rem auto;
      padding: 1rem;
      background: #fff;
      border-radius: 8px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    h1 {
      text-align: center;
      color: #333;
    }
    form {
      display: flex;
      flex-direction: column;
      margin-bottom: 1.5rem;
    }
    input, textarea, button {
      font-size: 1rem;
      padding: 0.8rem;
      margin-bottom: 1rem;
      border: 1px solid #ddd;
      border-radius: 5px;
    }
    textarea {
      resize: none;
      height: 100px;
    }
    button {
      background: #007bff;
      color: white;
      border: none;
      cursor: pointer;
    }
    button:hover {
      background: #0056b3;
    }
    .messages {
      margin-top: 1.5rem;
    }
    .message {
      padding: 1rem;
      border-bottom: 1px solid #ddd;
    }
    .message:last-child {
      border-bottom: none;
    }
    .message p {
      margin: 0.5rem 0;
    }
    .meta {
      font-size: 0.9rem;
      color: #555;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Message Board</h1>
    <form id="messageForm">
      <input type="text" id="name" placeholder="Your Name" required>
      <textarea id="message" placeholder="Write your message here..." required></textarea>
      <button type="submit">Post Message</button>
    </form>
    <div class="messages" id="messages">
      <!-- Messages will appear here -->
    </div>
  </div>
</body>
</html>
