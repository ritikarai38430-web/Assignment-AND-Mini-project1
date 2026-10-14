Mini-project1

# MINI PROJECT
const inventory = [
    { name: "Keyboard", price: 800 },
    { name: "Monitor", price: 5000 },
    { name: "Mouse", price: 400 }
];

// Function to classify products
const getCategory = (price) => {
    if (price <= 1000) {
        return "Budget";
    } else {
        return "Premium";
    }
};

// Function to add a product
function addProduct() {
    let name = prompt("Enter product name:");
    let price = Number(prompt("Enter product price:"));

    if (name === null || name.trim() === "" ||
        !Number.isFinite(price) || price <= 0) {
        console.log("Invalid product details!");
        return;
    }

    inventory.push({ name: name.trim(), price: price });
    console.log("Product added successfully!");
}

// Function to display inventory
function showInventory() {
    let total = 0;

    for (const product of inventory) {
        if (!product.name) continue;

        console.log(
            `${product.name} - ₹${product.price} - ${getCategory(product.price)}`
        );

        total += product.price;
    }

    console.log(`Total Inventory Value: ₹${total}`);
}

// Function to calculate tax and discount
const calculateFinalPrice = (total, tax, discount) => {
    let taxAmount = total * tax / 100;
    let discountAmount = total * discount / 100;

    return total + taxAmount - discountAmount;
};

// Main menu
while (true) {
    let choice = prompt(
        "1. Add Product\n2. View Inventory\n3. Calculate Final Price\n4. Exit"
    );

    if (choice === null) break;

    switch (choice.trim()) {
        case "1":
            addProduct();
            break;

        case "2":
            showInventory();
            break;

        case "3": {
            let total = inventory.reduce((sum, p) => sum + p.price, 0);
            let finalPrice = calculateFinalPrice(total, 18, 5);
            console.log(`Final Price after tax and discount: ₹${finalPrice}`);
            break;
        }

        case "4":
            console.log("Thank you!");
            break;

        default:
            console.log("Invalid choice!");
            continue;
    }

    if (choice.trim() === "4") break;
}

