---
layout: default
title: "Create a New Post"
permalink: /newposts/
---

<style>
  body {
    min-height: 100vh;
    margin: 0;
    background-size: cover;
    background-attachment: fixed;
  }

  .new-post-form {
    max-width: 800px;
    color: red;
    margin: 2em auto;
    padding: 20px;
    background-color: transparent;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }

  .new-post-form h2,
  .form-group label,
  .form-group input,
  .form-group textarea {
    color: red;
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
    background-color: #111;
    color: red;
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
    background-color: rgb(5, 29, 54);
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

    <div class="form-group">
      <label for="code">Code (optional):</label>
      <textarea id="code" name="code" placeholder="Paste any code to include in the post" rows="6"></textarea>
    </div>

    <button type="submit" class="submit-btn">Post</button>
  </form>
</div>

<script>
document.getElementById('newPostForm').addEventListener('submit', function(event) {
  event.preventDefault();

  const token = localStorage.getItem('githubToken');
  if (!token) {
    alert("No GitHub token found. Run in browser console:\n\nlocalStorage.setItem('githubToken', 'YOUR_TOKEN_HERE')");
    return;
  }

  const title = document.getElementById('title').value.trim();
  const content = document.getElementById('content').value.trim();
  const code = document.getElementById('code').value.trim();

  if (!title || !content) {
    alert("Title and content are required.");
    return;
  }

  const date = new Date();
  const dateStr = date.toISOString().split("T")[0];
  const postname = title.toLowerCase().replace(/\s+/g, '-').replace(/[^\w\-]+/g, '');
  const filename = `${dateStr}-${postname}.md`;

  let postContent = `---\nlayout: post\ntitle: "${title}"\ndate: ${date.toISOString()}\n---\n\n${content}`;

  if (code) {
    const escapedCode = code
      .replace(/&/g, '&amp;')
      .replace(/</g, '&lt;')
      .replace(/>/g, '&gt;');

    // Embed code block with copy functionality
    postContent += `
<div style="position: relative; background: #1e1e1e; padding: 1em; border-radius: 8px; font-family: monospace; white-space: pre-wrap; word-wrap: break-word; color: #f8f8f2; border: 1px solid #444;">
  <button onclick="copyCodeBlock(this)" style="position: absolute; top: 10px; right: 10px; padding: 4px 8px; font-size: 0.8em; background: #444; color: #fff; border: none; border-radius: 4px; cursor: pointer;">Copy</button>
  <code>${escapedCode}</code>
</div>

<script>
function copyCodeBlock(button) {
  const code = button.nextElementSibling.innerText;
  navigator.clipboard.writeText(code).then(() => alert("Copied!"));
}
</script>`;
  }

  const payload = {
    message: `Create new post: ${title}`,
    content: btoa(unescape(encodeURIComponent(postContent))),
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
