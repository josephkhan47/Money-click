<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Earnings App</title>
    <script src="https://www.paypal.com/sdk/js?ARg7kZRpcfGcNdz8peLfy_-iGP5VISNghrjy0XnYs08fnztE93TbOIFfnnhNvpDUFZ81dgOwmST-BkID"></script> <!-- Replace with your actual Client ID -->
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }
        button {
            margin: 10px;
            padding: 10px 20px;
            font-size: 16px;
        }
    </style>
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

    <script>
        let earnings = 0;

        // Update earnings display
        function updateEarnings() {
            document.getElementById('earnings').innerText = (earnings / 100).toFixed(2);
        }

        // Handle earning button click
        document.getElementById('earn-button').addEventListener('click', function() {
            earnings += 50; // Add 50 pence
            updateEarnings();
        });

        // Handle cash out button click
        document.getElementById('cashout-button').addEventListener('click', function() {
            if (earnings <= 0) {
                alert('You have no earnings to cash out!');
                return; // Exit the function if no earnings
            }
            document.getElementById('paypal-button-container').style.display = 'block';

            // Render the PayPal button
            paypal.Buttons({
                createOrder: function(data, actions) {
                    return actions.order.create({
                        purchase_units: [{
                            amount: {
                                value: (earnings / 100).toFixed(2) // Convert to pounds
                            }
                        }]
                    });
                },
                onApprove: function(data, actions) {
                    return actions.order.capture().then(function(details) {
                        alert('Transaction completed by ' + details.payer.name.given);
                        // Handle successful transaction here (reset earnings, etc.)
                        earnings = 0; // Reset earnings after cashout
                        updateEarnings();
                        document.getElementById('paypal-button-container').style.display = 'none'; // Hide the button after cashout
                    });
                },
                onError: function(err) {
                    console.error('PayPal Checkout onError', err);
                    alert('An error occurred during the transaction. Please try again.');
                }
            }).render('#paypal-button-container'); // Render the PayPal button
        });
    </script>
</body>
</html>
    
