---
layout: default
title: "Create a New Post"
permalink: /newposts/
---

<style>
  .new-post-form {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    background-color: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }

  .new-post-form h2 {
    text-align: center;
    font-size: 2rem;
    margin-bottom: 20px;
  }

  .form-group {
    margin-bottom: 15px;
  }

  .form-group label {
    font-weight: bold;
    display: block;
    margin-bottom: 5px;
  }

  .form-group input,
  .form-group textarea {
    width: 100%;
    padding: 10px;
    font-size: 1rem;
    border: 1px solid #ccc;
    border-radius: 4px;
  }

  .form-group textarea {
    resize: vertical;
  }

  .form-group input:focus,
  .form-group textarea:focus {
    border-color: #007BFF;
    outline: none;
  }

  .submit-btn {
    display: block;
    width: 100%;
    padding: 12px;
    font-size: 1.1rem;
    background-color: #007BFF;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .submit-btn:hover {
    background-color: #0056b3;
  }
</style>

<div class="new-post-form">
  <h2>Create a New Post</h2>
  <form id="newPostForm">
    <div class="form-group">
      <label for="title">Title:</label>
      <input type="text" id="title" name="title" placeholder="Enter the post title" required>
    </div>

    <div class="form-group">
      <label for="content">Content:</label>
      <textarea id="content" name="content" placeholder="Write your post content here" rows="10" required></textarea>
    </div>

    <button type="submit" class="submit-btn">Submit Post</button>
  </form>
</div>

<script>
document.getElementById('newPostForm').addEventListener('submit', function(event) {
  event.preventDefault();

  const token = localStorage.getItem('githubToken'); // Securely get token from browser storage

  if (!token) {
    alert("No GitHub token found. Please run this in your browser console first:\n\nlocalStorage.setItem('githubToken', 'YOUR_TOKEN_HERE')");
    return;
  }

  const title = document.getElementById('title').value.trim();
  const content = document.getElementById('content').value.trim();

  if (!title || !content) {
    alert("Both title and content are required.");
    return;
  }

  const date = new Date();
  const dateStr = date.toISOString().split("T")[0]; // YYYY-MM-DD
  const postname = title.toLowerCase().replace(/\s+/g, '').replace(/[^\w\-]+/g, '');
  const filename = `${dateStr}-${postname}.md`;

  const postContent = `---
layout: post
title: "${title}"
date: ${date.toISOString()}
---
${content}`;

  const payload = {
    message: `Create new post: ${title}`,
    content: btoa(postContent),
    branch: "main"
  };

  fetch(`https://api.github.com/repos/Yousuf200/Yousuf200.github.io/contents/_posts/${filename}`, {
    method: "PUT",
    headers: {
      "Authorization": "token " + token,
      "Content-Type": "application/json"
    },
    body: JSON.stringify(payload)
  })
  .then(res => res.json())
  .then(data => {
    if (data.content) {
      alert("✅ Post created successfully!");
      window.location.href = "/";
    } else {
      console.error(data);
      alert("❌ Error creating post:\n" + (data.message || "Unknown error"));
    }
  })
  .catch(err => {
    console.error(err);
    alert("❌ Request failed: " + err.message);
  });
});
</script>
