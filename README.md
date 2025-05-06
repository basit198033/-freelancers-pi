# -freelancers-pi
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Freelancers Pi</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Welcome to Freelancers Pi</h1>
        <button onclick="connectWallet()">Connect Pi Wallet</button>
    </header>

    <section id="services">
        <h2>Available Services</h2>
        <div class="service-list">
            <!-- List services dynamically from the database -->
        </div>
    </section>

    <section id="profile">
        <h2>Your Profile</h2>
        <p id="user-info">No user connected</p>
    </section>

    <footer>
        <p>&copy; 2025 Freelancers Pi</p>
    </footer>

    <script src="https://cdn.jsdelivr.net/npm/@minepi/pi-sdk@2.0.0-beta.6"></script>
    <script src="app.js"></script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f0f4f8;
}

header {
    background-color: #4CAF50;
    color: white;
    padding: 10px;
    text-align: center;
}

#services {
    padding: 20px;
    margin: 10px;
}

.service-list {
    display: flex;
    flex-wrap: wrap;
}

.service {
    background-color: white;
    padding: 15px;
    margin: 10px;
    border-radius: 5px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    width: 200px;
    text-align: center;
}

button {
    padding: 10px;
    background-color: #4CAF50;
    border: none;
    color: white;
    cursor: pointer;
}

button:hover {
    background-color: #45a049;
}
// Initialize Pi SDK
Pi.init({
    version: "2.0",
    sandbox: true,
}).then(() => {
    console.log("Pi SDK initialized successfully");
});

// Function to connect to Pi Wallet
function connectWallet() {
    Pi.login().then((user) => {
        console.log('User connected:', user);
        document.getElementById("user-info").innerText = `Hello, ${user.username}`;
        // Now you can perform Pi-related transactions
    }).catch((error) => {
        console.error("Error connecting wallet:", error);
    });
}


// Static list of services (replace with database later)
const services = [
    { name: "Graphic Design", price: "10 Pi" },
    { name: "Web Development", price: "20 Pi" },
    { name: "Content Writing", price: "5 Pi" }
];

// Display services dynamically
const serviceList = document.querySelector('.service-list');
services.forEach(service => {
    const serviceItem = document.createElement('div');
    serviceItem.classList.add('service');
    serviceItem.innerHTML = `
        <h3>${service.name}</h3>
        <p>Price: ${service.price}</p>
        <button onclick="buyService('${service.name}')">Buy Service</button>
    `;
    serviceList.appendChild(serviceItem);
});

// Function to handle service purchase
function buyService(serviceName) {
    alert(`You have purchased ${serviceName}!`);
    // You can add actual Pi transaction logic here
}





