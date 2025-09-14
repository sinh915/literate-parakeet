// server.js
const express = require("express");
const bodyParser = require("body-parser");
const app = express();

app.use(bodyParser.urlencoded({ extended: true }));

// Example users (username: password)
const users = {
  "user1": "1234",
  "user2": "abcd"
};

// Serve static HTML files
app.use(express.static(__dirname));

// Handle login
app.post("/login", (req, res) => {
  const { username, password } = req.body;
  if (users[username] && users[username] === password) {
    res.send(`<h1>Welcome ${username}!</h1><p>Here is your information: This is secret content.</p>`);
  } else {
    res.send("<h1>Login failed</h1><p>Invalid username or password.</p>");
  }
});

// Start server
const port = process.env.PORT || 3000;
app.listen(port, () => console.log(`Server running on port ${port}`));
