<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Shared Message Board</title>
  <style>
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

  <script>
    // Initialize messages from localStorage
    const messages = JSON.parse(localStorage.getItem('messages')) || [];

    // Function to render messages
    function renderMessages() {
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

    // Render messages on load
    renderMessages();

    // Handle form submission
    document.getElementById('messageForm').addEventListener('submit', function (e) {
      e.preventDefault();

      // Get form values
      const name = document.getElementById('name').value.trim();
      const text = document.getElementById('message').value.trim();
      const date = new Date().toLocaleString();

      // Add message to array
      const newMessage = { name, text, date };
      messages.push(newMessage);

      // Save to localStorage
      localStorage.setItem('messages', JSON.stringify(messages));

      // Render messages
      renderMessages();

      // Clear form
      document.getElementById('name').value = '';
      document.getElementById('message').value = '';
    });
  </script>
</body>
</html
