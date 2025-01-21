<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Social Network</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f0f2f5;
        }

        .navbar {
            background-color: #4267B2;
            color: white;
            padding: 10px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .navbar h1 {
            margin: 0;
            font-size: 1.5em;
        }

        .navbar .search-bar {
            flex-grow: 1;
            margin: 0 20px;
        }

        .navbar .search-bar input {
            width: 100%;
            padding: 5px;
            border: none;
            border-radius: 5px;
        }

        .feed {
            max-width: 600px;
            margin: 20px auto;
            padding: 10px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .post {
            background: #f9f9f9;
            padding: 10px;
            margin: 10px 0;
            border-radius: 5px;
        }

        .create-post {
            margin-bottom: 20px;
        }

        .create-post textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            resize: none;
        }

        .create-post button {
            margin-top: 10px;
            padding: 10px 15px;
            border: none;
            border-radius: 5px;
            background: #4267B2;
            color: white;
            cursor: pointer;
        }

        .create-post button:hover {
            background: #365899;
        }

        .post-author {
            font-weight: bold;
        }

        .post-content {
            margin-top: 5px;
        }

        footer {
            text-align: center;
            margin-top: 20px;
            padding: 10px;
            background: #4267B2;
            color: white;
        }

        #username-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            display: flex;
            justify-content: center;
            align-items: center;
        }

        #username-modal .modal-content {
            background: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        }

        #username-modal input {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        #username-modal button {
            padding: 10px 15px;
            border: none;
            border-radius: 5px;
            background: #4267B2;
            color: white;
            cursor: pointer;
        }

        #username-modal button:hover {
            background: #365899;
        }
    </style>
</head>
<body>
    <!-- Username Modal -->
    <div id="username-modal">
        <div class="modal-content">
            <h2>Enter Your Name</h2>
            <input type="text" id="username" placeholder="Your name">
            <button onclick="enterSite()">Enter</button>
        </div>
    </div>

    <!-- Navbar -->
    <div class="navbar">
        <h1>SocialNet</h1>
        <div class="search-bar">
            <input type="text" placeholder="Search...">
        </div>
        <div class="profile">
            <a href="#" style="color: white; text-decoration: none;" id="display-username"></a>
        </div>
    </div>

    <!-- Feed -->
    <div class="feed">
        <div class="create-post">
            <textarea rows="3" placeholder="What's on your mind?" id="post-content"></textarea>
            <button onclick="createPost()">Post</button>
        </div>

        <div id="posts">
            <!-- Posts will appear here -->
        </div>
    </div>

    <footer>
        &copy; 2025 SocialNet. All rights reserved.
    </footer>

    <script>
        let username = '';

        function enterSite() {
            const nameInput = document.getElementById('username').value.trim();
            if (nameInput === '') {
                alert('Please enter your name!');
                return;
            }
            username = nameInput;
            document.getElementById('username-modal').style.display = 'none';
            document.getElementById('display-username').textContent = username;
        }

        function createPost() {
            const postContent = document.getElementById('post-content').value;
            if (postContent.trim() === '') {
                alert('Post cannot be empty!');
                return;
            }

            const postsContainer = document.getElementById('posts');

            const postElement = document.createElement('div');
            postElement.className = 'post';

            const postAuthor = document.createElement('div');
            postAuthor.className = 'post-author';
            postAuthor.textContent = username || 'Anonymous';

            const postText = document.createElement('div');
            postText.className = 'post-content';
            postText.textContent = postContent;

            postElement.appendChild(postAuthor);
            postElement.appendChild(postText);

            postsContainer.prepend(postElement);

            document.getElementById('post-content').value = '';
        }
    </script>
</body>
</html>
