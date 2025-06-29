<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LocalMart - Your Neighborhood Store Online</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Header */
        header {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            padding: 1rem 0;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1);
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: bold;
            color: #667eea;
        }

        .nav-links {
            display: flex;
            list-style: none;
            gap: 2rem;
        }

        .nav-links a {
            text-decoration: none;
            color: #333;
            font-weight: 500;
            transition: color 0.3s;
        }

        .nav-links a:hover {
            color: #667eea;
        }

        .cart-icon {
            position: relative;
            cursor: pointer;
            font-size: 1.5rem;
            color: #667eea;
        }

        .cart-count {
            position: absolute;
            top: -8px;
            right: -8px;
            background: #ff4757;
            color: white;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.8rem;
            font-weight: bold;
        }

        /* Hero Section */
        .hero {
            text-align: center;
            padding: 4rem 0;
            color: white;
        }

        .hero h1 {
            font-size: 3rem;
            margin-bottom: 1rem;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }

        .hero p {
            font-size: 1.2rem;
            margin-bottom: 2rem;
            opacity: 0.9;
        }

        /* Search and Filter */
        .search-filter {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            padding: 2rem;
            margin: 2rem 0;
            border-radius: 15px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        }

        .search-bar {
            display: flex;
            gap: 1rem;
            margin-bottom: 1rem;
            flex-wrap: wrap;
        }

        .search-bar input, .search-bar select {
            padding: 0.8rem;
            border: 2px solid #e1e8ed;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s;
        }

        .search-bar input {
            flex: 1;
            min-width: 250px;
        }

        .search-bar input:focus, .search-bar select:focus {
            outline: none;
            border-color: #667eea;
        }

        .price-filter {
            display: flex;
            gap: 1rem;
            align-items: center;
            flex-wrap: wrap;
        }

        /* Products Grid */
        .products-section {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            padding: 2rem;
            margin: 2rem 0;
            border-radius: 15px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        }

        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
            margin-top: 2rem;
        }

        .product-card {
            background: white;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s, box-shadow 0.3s;
        }

        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.15);
        }

        .product-image {
            width: 100%;
            height: 200px;
            background: linear-gradient(45deg, #f0f2f5, #e1e8ed);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
            color: #667eea;
        }

        .product-info {
            padding: 1.5rem;
        }

        .product-info h3 {
            margin-bottom: 0.5rem;
            color: #333;
        }

        .product-info p {
            color: #666;
            margin-bottom: 1rem;
            font-size: 0.9rem;
        }

        .product-price {
            font-size: 1.2rem;
            font-weight: bold;
            color: #667eea;
            margin-bottom: 1rem;
        }

        .add-to-cart {
            width: 100%;
            padding: 0.8rem;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.2s;
        }

        .add-to-cart:hover {
            transform: scale(1.02);
        }

        /* Cart Modal */
        .cart-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
        }

        .cart-content {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 2rem;
            border-radius: 15px;
            max-width: 500px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
        }

        .cart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
            padding-bottom: 1rem;
            border-bottom: 2px solid #f0f2f5;
        }

        .close-cart {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #666;
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem;
            border-bottom: 1px solid #f0f2f5;
        }

        .cart-total {
            text-align: center;
            margin-top: 1rem;
            padding-top: 1rem;
            border-top: 2px solid #f0f2f5;
        }

        .checkout-btn {
            width: 100%;
            padding: 1rem;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            margin-top: 1rem;
        }

        /* Footer */
        footer {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            text-align: center;
            padding: 2rem 0;
            margin-top: 3rem;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .hero h1 {
                font-size: 2rem;
            }
            
            .nav-links {
                display: none;
            }
            
            .search-bar {
                flex-direction: column;
            }
            
            .price-filter {
                flex-direction: column;
                align-items: stretch;
            }
        }
    </style>
</head>
<body>
    <header>
        <nav class="container">
            <div class="logo">🏪 LocalMart</div>
            <ul class="nav-links">
                <li><a href="#home">Home</a></li>
                <li><a href="#products">Products</a></li>
                <li><a href="#about">About</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
            <div class="cart-icon" onclick="toggleCart()">
                🛒
                <span class="cart-count" id="cartCount">0</span>
            </div>
        </nav>
    </header>

    <main>
        <section class="hero">
            <div class="container">
                <h1>Welcome to LocalMart</h1>
                <p>Your neighborhood store, now online. Fresh products delivered to your door!</p>
            </div>
        </section>

        <section class="container">
            <div class="search-filter">
                <h2>Find Your Products</h2>
                <div class="search-bar">
                    <input type="text" id="searchInput" placeholder="Search products..." onkeyup="filterProducts()">
                    <select id="categoryFilter" onchange="filterProducts()">
                        <option value="">All Categories</option>
                        <option value="groceries">Groceries</option>
                        <option value="electronics">Electronics</option>
                        <option value="clothing">Clothing</option>
                        <option value="home">Home & Garden</option>
                    </select>
                </div>
                <div class="price-filter">
                    <label>Price Range:</label>
                    <input type="range" id="minPrice" min="0" max="1000" value="0" onchange="filterProducts()">
                    <span id="minPriceDisplay">₹0</span>
                    <span> - </span>
                    <input type="range" id="maxPrice" min="0" max="1000" value="1000" onchange="filterProducts()">
                    <span id="maxPriceDisplay">₹1000</span>
                </div>
            </div>

            <div class="products-section">
                <h2>Our Products</h2>
                <div class="products-grid" id="productsGrid">
                    <!-- Products will be dynamically loaded here -->
                </div>
            </div>
        </section>
    </main>

    <!-- Cart Modal -->
    <div class="cart-modal" id="cartModal">
        <div class="cart-content">
            <div class="cart-header">
                <h3>Shopping Cart</h3>
                <button class="close-cart" onclick="toggleCart()">×</button>
            </div>
            <div id="cartItems">
                <p>Your cart is empty</p>
            </div>
            <div class="cart-total">
                <h3>Total: ₹<span id="cartTotal">0</span></h3>
                <button class="checkout-btn" onclick="checkout()">Proceed to Checkout</button>
            </div>
        </div>
    </div>

    <footer>
        <div class="container">
            <p>&copy; 2024 LocalMart. Bringing your neighborhood closer to you.</p>
        </div>
    </footer>

    <script>
        // Sample product data
        const products = [
            { id: 1, name: "Fresh Apples", category: "groceries", price: 120, image: "🍎", description: "Crisp and sweet red apples, locally sourced" },
            { id: 2, name: "Wireless Headphones", category: "electronics", price: 2499, image: "🎧", description: "High-quality bluetooth headphones with noise cancellation" },
            { id: 3, name: "Cotton T-Shirt", category: "clothing", price: 599, image: "👕", description: "Comfortable 100% cotton t-shirt in various colors" },
            { id: 4, name: "Indoor Plant", category: "home", price: 350, image: "🪴", description: "Beautiful indoor plant to brighten up your home" },
            { id: 5, name: "Organic Rice", category: "groceries", price: 80, image: "🌾", description: "Premium quality organic basmati rice" },
            { id: 6, name: "Smartphone", category: "electronics", price: 15999, image: "📱", description: "Latest smartphone with advanced features" },
            { id: 7, name: "Jeans", category: "clothing", price: 1299, image: "👖", description: "Stylish denim jeans with perfect fit" },
            { id: 8, name: "Table Lamp", category: "home", price: 899, image: "💡", description: "Modern LED table lamp with adjustable brightness" },
            { id: 9, name: "Fresh Milk", category: "groceries", price: 55, image: "🥛", description: "Fresh dairy milk delivered daily" },
            { id: 10, name: "Laptop", category: "electronics", price: 45999, image: "💻", description: "High-performance laptop for work and entertainment" },
            { id: 11, name: "Sneakers", category: "clothing", price: 2999, image: "👟", description: "Comfortable sports sneakers for daily wear" },
            { id: 12, name: "Coffee Maker", category: "home", price: 3499, image: "☕", description: "Automatic coffee maker for perfect morning brew" }
        ];

        let cart = [];
        let filteredProducts = [...products];

        // Initialize the page
        function init() {
            displayProducts(products);
            updatePriceDisplays();
        }

        // Display products
        function displayProducts(productsToShow) {
            const grid = document.getElementById('productsGrid');
            grid.innerHTML = '';

            productsToShow.forEach(product => {
                const productCard = document.createElement('div');
                productCard.className = 'product-card';
                productCard.innerHTML = `
                    <div class="product-image">${product.image}</div>
                    <div class="product-info">
                        <h3>${product.name}</h3>
                        <p>${product.description}</p>
                        <div class="product-price">₹${product.price}</div>
                        <button class="add-to-cart" onclick="addToCart(${product.id})">Add to Cart</button>
                    </div>
                `;
                grid.appendChild(productCard);
            });
        }

        // Filter products
        function filterProducts() {
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            const category = document.getElementById('categoryFilter').value;
            const minPrice = parseInt(document.getElementById('minPrice').value);
            const maxPrice = parseInt(document.getElementById('maxPrice').value);

            filteredProducts = products.filter(product => {
                const matchesSearch = product.name.toLowerCase().includes(searchTerm) || 
                                    product.description.toLowerCase().includes(searchTerm);
                const matchesCategory = !category || product.category === category;
                const matchesPrice = product.price >= minPrice && product.price <= maxPrice;

                return matchesSearch && matchesCategory && matchesPrice;
            });

            displayProducts(filteredProducts);
            updatePriceDisplays();
        }

        // Update price range displays
        function updatePriceDisplays() {
            const minPrice = document.getElementById('minPrice').value;
            const maxPrice = document.getElementById('maxPrice').value;
            document.getElementById('minPriceDisplay').textContent = `₹${minPrice}`;
            document.getElementById('maxPriceDisplay').textContent = `₹${maxPrice}`;
        }

        // Add to cart
        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            const existingItem = cart.find(item => item.id === productId);

            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                cart.push({ ...product, quantity: 1 });
            }

            updateCartDisplay();
            updateCartCount();
        }

        // Update cart count
        function updateCartCount() {
            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            document.getElementById('cartCount').textContent = totalItems;
        }

        // Update cart display
        function updateCartDisplay() {
            const cartItems = document.getElementById('cartItems');
            const cartTotal = document.getElementById('cartTotal');

            if (cart.length === 0) {
                cartItems.innerHTML = '<p>Your cart is empty</p>';
                cartTotal.textContent = '0';
                return;
            }

            cartItems.innerHTML = '';
            let total = 0;

            cart.forEach(item => {
                const cartItem = document.createElement('div');
                cartItem.className = 'cart-item';
                cartItem.innerHTML = `
                    <div>
                        <strong>${item.name}</strong><br>
                        ₹${item.price} x ${item.quantity}
                    </div>
                    <div>
                        <button onclick="changeQuantity(${item.id}, -1)">-</button>
                        <span style="margin: 0 10px;">${item.quantity}</span>
                        <button onclick="changeQuantity(${item.id}, 1)">+</button>
                        <button onclick="removeFromCart(${item.id})" style="margin-left: 10px; color: red;">×</button>
                    </div>
                `;
                cartItems.appendChild(cartItem);
                total += item.price * item.quantity;
            });

            cartTotal.textContent = total;
        }

        // Change quantity
        function changeQuantity(productId, change) {
            const item = cart.find(item => item.id === productId);
            if (item) {
                item.quantity += change;
                if (item.quantity <= 0) {
                    removeFromCart(productId);
                } else {
                    updateCartDisplay();
                    updateCartCount();
                }
            }
        }

        // Remove from cart
        function removeFromCart(productId) {
            cart = cart.filter(item => item.id !== productId);
            updateCartDisplay();
            updateCartCount();
        }

        // Toggle cart modal
        function toggleCart() {
            const modal = document.getElementById('cartModal');
            modal.style.display = modal.style.display === 'block' ? 'none' : 'block';
        }

        // Checkout
        function checkout() {
            if (cart.length === 0) {
                alert('Your cart is empty!');
                return;
            }

            const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            alert(`Thank you for your order! Total: ₹${total}\n\nYour order will be processed and delivered soon.`);
            
            // Clear cart
            cart = [];
            updateCartDisplay();
            updateCartCount();
            toggleCart();
        }

        // Close modal when clicking outside
        window.onclick = function(event) {
            const modal = document.getElementById('cartModal');
            if (event.target === modal) {
                modal.style.display = 'none';
            }
        }

        // Initialize the page
        init();
    </script>
</body>
</html>
