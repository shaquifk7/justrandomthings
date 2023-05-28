# justrandomthings
const express = require('express');
const fileUpload = require('express-fileupload');
const app = express();

// Use fileUpload middleware
app.use(fileUpload());

// Serve the HTML file
app.get('/', (req, res) => {
  res.sendFile(__dirname + '/index.html');
});

// Handle the file upload
app.post('/upload', (req, res) => {
  if (!req.files || Object.keys(req.files).length === 0) {
    return res.status(400).send('No files were uploaded.');
  }

  const file = req.files.file;
  // Process the file as per your requirements
  // For example, you can save it to a directory:
  file.mv('uploads/' + file.name, (err) => {
    if (err) {
      return res.status(500).send(err);
    }
    res.send('File uploaded successfully!');
  });
});

// Start the server
const port = 3000;
app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
