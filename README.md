<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Earnings App</title>
    <script src="https://www.paypal.com/sdk/js?client-id=YOUR_CLIENT_ID_HERE"></script> <!-- Replace YOUR_CLIENT_ID_HERE -->
    <link rel="stylesheet" href="styles.css"> <!-- Optional: Link to a CSS file for styling -->
</head>
<body>
    <h1>Earnings App</h1>
    <div id="earnings-display">
        <h2>Your Earnings: <span id="earnings">0.00</span> GBP</h2>
    </div>
    <button id="earn-button">Click to Earn 50p!</button>
    <br><br>
    <button id="cashout-button">Cash Out</button>

    <div id="paypal-button-container" style="display: none;"></div>

    <script src="index.js"></script> <!-- Link to your JavaScript file -->
</body>
</html>
