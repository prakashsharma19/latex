<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact Form</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      padding: 20px;
    }
    form {
      background-color: #fff;
      max-width: 500px;
      margin: 0 auto;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }
    label {
      display: block;
      margin-bottom: 10px;
      font-weight: bold;
    }
    input, textarea, button {
      width: 100%;
      padding: 10px;
      margin-bottom: 20px;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-size: 16px;
    }
    button {
      background-color: #4CAF50;
      color: white;
      border: none;
      cursor: pointer;
    }
    button:hover {
      background-color: #45a049;
    }
    .required:after {
      content: "*";
      color: red;
      margin-left: 5px;
    }
  </style>
</head>
<body>

  <form action="https://formspree.io/f/xgvwjkqz" method="POST">
    <label for="name" class="required">Your Name</label>
    <input type="text" id="name" name="name" required>

    <label for="email" class="required">Your Email</label>
    <input type="email" id="email" name="email" required>

    <label for="message">Your Message</label>
    <textarea id="message" name="message" rows="5"></textarea>

    <button type="submit">Send Message</button>
  </form>

</body>
</html>
