# BSVS-food-shop
<!DOCTYPE html>
<html>
<head>
    <title>BSVS Food Shop</title>
    <style>
        body {
            font-family: Arial;
            text-align: center;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }

        .page {
            display: none;
            padding: 40px;
        }

        h1, h2 {
            color: #333;
        }

        button {
            padding: 10px 20px;
            background-color: orange;
            border: none;
            color: white;
            font-size: 16px;
            cursor: pointer;
            margin-top: 20px;
        }

        button:hover {
            background-color: darkorange;
        }

        .food-item {
            margin: 8px;
        }

        #foodList {
            margin-top: 20px;
        }

        .summary-box {
            background: white;
            padding: 20px;
            width: 60%;
            margin: auto;
            border-radius: 10px;
            box-shadow: 0px 0px 10px #ccc;
        }
    </style>
</head>
<body>

<!-- 1️⃣ Welcome Page -->
<div id="welcomePage" class="page" style="display:block;">
    <h1>Welcome to BSVS Food Shop 🍔</h1>
    <button onclick="showOrderPage()">Order Now</button>
</div>

<!-- 2️⃣ Order Page -->
<div id="orderPage" class="page">
    <h2>Select Your Junk Food</h2>
    <div id="foodList"></div>
    <button onclick="placeOrder()">Place Order</button>
</div>

<!-- 3️⃣ Summary Page -->
<div id="summaryPage" class="page">
    <h2>Order Summary</h2>
    <div id="summaryContent" class="summary-box"></div>
    <button onclick="goHome()">Back to Home</button>
</div>

<script>
    const foods = [
        {name: "Burger", price: 120},
        {name: "Pizza", price: 250},
        {name: "French Fries", price: 100},
        {name: "Sandwich", price: 90},
        {name: "Hot Dog", price: 110},
        {name: "Fried Chicken", price: 180},
        {name: "Noodles", price: 130},
        {name: "Pasta", price: 150},
        {name: "Tacos", price: 140},
        {name: "Nachos", price: 120},
        {name: "Popcorn", price: 80},
        {name: "Donut", price: 60},
        {name: "Ice Cream", price: 70},
        {name: "Milkshake", price: 90},
        {name: "Chips", price: 50},
        {name: "Samosa", price: 30},
        {name: "Rolls", price: 100},
        {name: "Momos", price: 120},
        {name: "Brownie", price: 85},
        {name: "Cupcake", price: 75}
    ];

    // Load food items
    const foodListDiv = document.getElementById("foodList");
    foods.forEach((food, index) => {
        foodListDiv.innerHTML += `
            <div class="food-item">
                <input type="checkbox" value="${index}">
                ${food.name} - ₹${food.price}
            </div>
        `;
    });

    function showOrderPage() {
        document.getElementById("welcomePage").style.display = "none";
        document.getElementById("orderPage").style.display = "block";
    }

    function placeOrder() {
        const selected = document.querySelectorAll("input[type='checkbox']:checked");

        if (selected.length === 0) {
            alert("Please select at least one item!");
            return;
        }

        let total = 0;
        let orderedItems = [];

        selected.forEach(item => {
            const food = foods[item.value];
            orderedItems.push(food);
            total += food.price;
        });

        let prepTime = orderedItems.length * 5; // 5 minutes per item

        let summaryHTML = "<h3>Ordered Items:</h3><ul>";
        orderedItems.forEach(item => {
            summaryHTML += `<li>${item.name} - ₹${item.price}</li>`;
        });
        summaryHTML += `</ul>
                        <h3>Total Amount: ₹${total}</h3>
                        <h3>Preparation Time: ${prepTime} minutes</h3>`;

        document.getElementById("summaryContent").innerHTML = summaryHTML;

        // Simulated notification to kitchen
        alert("🔔 Notification Sent to Kitchen!\nOrdered Items:\n" + 
              orderedItems.map(i => i.name).join(", "));

        document.getElementById("orderPage").style.display = "none";
        document.getElementById("summaryPage").style.display = "block";
    }

    function goHome() {
        location.reload();
    }
</script>

</body>
</html>
