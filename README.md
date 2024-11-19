# Project Responsive Web Design using Bootstrap
## Date:18-11-2024

## AIM:
To create a simplified clone of Dribbble (https://dribbble.com/) landing page.


## DESIGN STEPS:

### Step 1:
Clone the repository from GitHub.

### Step 2:
Create Django Admin project.

### Step 3:
Create a New App under the Django Admin project.

### Step 4:
Insert the necessary CSS and JavaScript files as external in order to use Bootstrap.

### Step 5:
Create a HTML file and include the needed Bootstrap components.

### Step 6:
Publish the website in the LocalHost.

## PROGRAM :

## HTML

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive E-Commerce Website</title>
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- Custom CSS -->
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <!-- Navbar -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <div class="container">
            <a class="navbar-brand" href="#">INDIAN STORE</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <!-- Centered Search Bar -->
                <form class="d-flex mx-auto" role="search">
                    <input class="form-control me-2" type="search" placeholder="Search products..." aria-label="Search">
                    <button class="btn btn-outline-light" type="submit">Search</button>
                </form>
                <!-- Right-aligned Buttons -->
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item">
                        <button class="btn btn-outline-light me-2" onclick="alert('Signup page coming soon!')">Signup</button>
                    </li>
                    <li class="nav-item">
                        <button class="btn btn-outline-light" onclick="alert('Login page coming soon!')">Login</button>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <header class="text-center bg-light py-5">
        <div class="container">
            <h1>Welcome to INDIAN STORE</h1>
            <p class="lead">Discover the best deals and products tailored just for you!</p>
        </div>
    </header>

    <!-- Products Section -->
    <section id="products" class="py-5">
        <div class="container">
            <h2 class="text-center mb-4">Our Products</h2>
            <div class="row" id="productList">
                <!-- Example Product -->
                <div class="col-sm-6 col-md-4 product">
                    <div class="card">
                        <img src="1.jpg" class="card-img-top" alt="Product 1">
                        <div class="card-body text-center">
                            <h5 class="card-title">Blazers</h5>
                            <p class="card-text">$100</p>
                            <button class="btn btn-primary add-to-cart" data-name="Product 1" data-price="10">Add to Cart</button>
                        </div>
                    </div>
                </div>
                <div class="col-sm-6 col-md-4 product">
                    <div class="card">
                        <img src="2.jpg" class="card-img-top" alt="Product 2">
                        <div class="card-body text-center">
                            <h5 class="card-title">Hoodie</h5>
                            <p class="card-text">$80</p>
                            <button class="btn btn-primary add-to-cart" data-name="Product 2" data-price="20">Add to Cart</button>
                        </div>
                    </div>
                </div>
                <div class="col-sm-6 col-md-4 product">
                    <div class="card">
                        <img src="3.png" class="card-img-top" alt="Product 3">
                        <div class="card-body text-center">
                            <h5 class="card-title">T-Shirt</h5>
                            <p class="card-text">$55</p>
                            <button class="btn btn-primary add-to-cart" data-name="Product 3" data-price="30">Add to Cart</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Cart Section -->
    <section id="cart" class="py-5 bg-light">
        <div class="container">
            <h2 class="text-center mb-4">Shopping Cart</h2>
            <table class="table table-bordered">
                <thead>
                    <tr>
                        <th>Product</th>
                        <th>Price</th>
                        <th>Quantity</th>
                        <th>Total</th>
                        <th>Action</th>
                    </tr>
                </thead>
                <tbody id="cartItems">
                    <tr>
                        <td colspan="5" class="text-center">Your cart is empty</td>
                    </tr>
                </tbody>
            </table>
            <h3 class="text-end">Total: $<span id="cartTotal">0</span></h3>
        </div>
    </section>

    <!-- Bootstrap JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
    <!-- Custom JS -->
    <script src="script.js"></script>
</body>
</html>
```




## script.js

```
// Shopping Cart Logic
const cart = [];
const cartItems = document.getElementById("cartItems");
const cartTotal = document.getElementById("cartTotal");

// Add to Cart Functionality
document.querySelectorAll(".add-to-cart").forEach((button) => {
    button.addEventListener("click", (event) => {
        const name = event.target.dataset.name;
        const price = parseFloat(event.target.dataset.price);

        // Check if the item already exists in the cart
        const existingItem = cart.find((item) => item.name === name);

        if (existingItem) {
            existingItem.quantity++;
        } else {
            cart.push({ name, price, quantity: 1 });
        }

        updateCart();
    });
});

// Update Cart Functionality
function updateCart() {
    cartItems.innerHTML = "";

    if (cart.length === 0) {
        cartItems.innerHTML = `<tr><td colspan="5" class="text-center">Your cart is empty</td></tr>`;
        cartTotal.textContent = "0";
        return;
    }

    let total = 0;

    cart.forEach((item, index) => {
        const itemTotal = item.price * item.quantity;
        total += itemTotal;

        const row = document.createElement("tr");
        row.innerHTML = `
            <td>${item.name}</td>
            <td>$${item.price.toFixed(2)}</td>
            <td>${item.quantity}</td>
            <td>$${itemTotal.toFixed(2)}</td>
            <td><button class="btn btn-danger btn-sm remove-item" data-index="${index}">Remove</button></td>
        `;
        cartItems.appendChild(row);
    });

    cartTotal.textContent = total.toFixed(2);

    // Add event listeners to remove buttons
    document.querySelectorAll(".remove-item").forEach((button) => {
        button.addEventListener("click", (event) => {
            const index = parseInt(event.target.dataset.index);
            cart.splice(index, 1);
            updateCart();
        });
    });
}
```




## CSS

```
body {
    font-family: 'Arial', sans-serif;
}

.navbar-brand {
    font-weight: bold;
    color: #f39c12 !important;
}

.card {
    border: none;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
    transform: scale(1.05);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

#cart h3 {
    font-weight: bold;
    color: #2ecc71;
}

```

## OUTPUT:
![Screenshot (346)](https://github.com/user-attachments/assets/b921c8eb-44a0-4b9b-a306-e9060c66fb29)
![Screenshot (347)](https://github.com/user-attachments/assets/8592fb00-e747-450c-9f7c-2ff809d57750)




## RESULT:
The Project for responsive web design using Bootstrap is completed successfully.
