# Introduction
This **Online Shopping Cart System** is a mini-project built using **Object-Oriented Programming (OOP)** concepts in Java. It demonstrates how core OOP principles like **encapsulation**, **inheritance**, and **polymorphism** can be applied to structure a simple shopping cart system. The project is designed to simulate an e-commerce experience where users can browse products, add items to their cart, remove items, view their cart, and proceed to checkout.

This system serves as a **dummy project** to demonstrate the fundamental OOP concepts in action and can be extended into a more robust and reliable shopping system with additional functionalities.

## Key Components
### Product Class
* Represents an item in the shop with attributes like `id`, `name`, `price`, and `quantity`.
* Contains getter and setter methods to access and modify these attributes.
* Includes a `displayProduct()` method to print product details.

```
public class Product {
    private String id;
    private String name;
    private double price;
    private int quantity;

    // Constructor
    public Product(String id, String name, double price, int quantity) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }

    // Getters and Setters
    public String getId() { return id; }
    public String getName() { return name; }
    public double getPrice() { return price; }
    public int getQuantity() { return quantity; }

    public void setQuantity(int quantity) { this.quantity = quantity; }
    
    // Display product information
    public void displayProduct() {
        System.out.println("Product ID: " + id + ", Name: " + name + ", Price: $" + price + ", Quantity: " + quantity);
    }
}
```

### Cart Class
* Manages the products added to the user’s cart.
* Provides methods to add, remove, and display products in the cart.
* Includes `calculateTotalCost()` to compute the total price of items in the cart.

```
import java.util.ArrayList;

public class Cart {
    private ArrayList<Product> products;

    // Constructor
    public Cart() {
        products = new ArrayList<>();
    }

    // Add product to cart with quantity
    public void addProduct(Product product, int quantity) {
        boolean found = false;

        // Check if the product is already in the cart
        for (Product p : products) {
            if (p.getId().equals(product.getId())) {
                p.setQuantity(p.getQuantity() + quantity);  // Increase quantity if already present
                found = true;
                System.out.println(quantity + " " + product.getName() + "(s) added to your cart. New quantity: " + p.getQuantity());
                break;
            }
        }

        // If product is not in the cart, add it with the specified quantity
        if (!found) {
            product.setQuantity(quantity);
            products.add(product);
            System.out.println(quantity + " " + product.getName() + "(s) added to your cart.");
        }
    }

    // Remove product from cart with quantity
    public void removeProduct(String productId, int quantity) {
        for (Product product : products) {
            if (product.getId().equals(productId)) {
                if (product.getQuantity() > quantity) {
                    product.setQuantity(product.getQuantity() - quantity);
                    System.out.println(quantity + " " + product.getName() + "(s) removed from your cart. Remaining quantity: " + product.getQuantity());
                } else {
                    products.remove(product);  // Remove product entirely if quantity is 0 or less
                    System.out.println(product.getName() + " removed from your cart.");
                }
                break;
            }
        }
    }

    // Display all products in the cart
    public void displayCart() {
        System.out.println("Cart Items:");
        for (Product product : products) {
            product.displayProduct();
        }
    }

    // Calculate total cost
    public double calculateTotalCost() {
        double total = 0;
        for (Product product : products) {
            total += product.getPrice() * product.getQuantity();
        }
        return total;
    }
}
```

### User Class
* Represents the customer shopping in the store.
* Each user has a `name` and their own `Cart` object to manage selected items.

```
public class User {
    private String name;
    private Cart cart;

    // Constructor
    public User(String name) {
        this.name = name;
        this.cart = new Cart();
    }

    // Getters
    public String getName() { return name; }
    public Cart getCart() { return cart; }
}
```

### Shop Class
* Manages the inventory of products available for purchase.
* Loads a selection of sample products and provides methods to display products and find specific products by their ID.

```
import java.util.ArrayList;

public class Shop {
    private ArrayList<Product> products;

    // Constructor
    public Shop() {
        products = new ArrayList<>();
        loadProducts();
    }

    // Load some products into the shop
    private void loadProducts() {
        products.add(new Product("P001", "Laptop", 899.99, 5));
        products.add(new Product("P002", "Smartphone", 599.99, 10));
        products.add(new Product("P003", "Headphones", 49.99, 20));
    }

    // Display available products in the shop
    public void displayProducts() {
        System.out.println("Available Products:");
        for (Product product : products) {
            product.displayProduct();
        }
    }

    // Find product by ID
    public Product findProduct(String id) {
        for (Product product : products) {
            if (product.getId().equals(id)) {
                return product;
            }
        }
        return null;
    }
}
```

### Main Class
* Simulates user interactions with the shop and the cart.
* Allows users to:
1. Add products to the cart by product ID and quantity.
2. Remove products from the cart.
3. View the items in their cart.
4. Checkout and display the total cost.
* The application runs in a loop, allowing users to continue shopping until they decide to checkout or exit.

```
import java.util.Scanner;

public class OnlineShoppingApp {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		Shop shop = new Shop();
		
		User user = new User("Nakul");
		
		boolean shopping = true;
		
		System.out.println("\nWelcome, " + user.getName());
		while(shopping) {
			shop.displayProduct();
			
			System.out.println("\n1. Add to Cart\n2. Remove from Cart\n3. View Cart\n4. Checkout\n5. Exit");
			int choice = scanner.nextInt();
			scanner.nextLine();
			
			switch(choice) {
			case 1: 
				System.out.println("Enter product id to add: ");
				String productId = scanner.nextLine();
				Product p = shop.findProductById(productId);
				
				if(null != p) {
					System.out.println("Enter quantity to add: ");
					int quantity = scanner.nextInt();
					scanner.nextLine();
					user.getCart().addProduct(p, quantity);
				}else {
					System.out.println("Product not found!!!");
				}
				
				break;
				
			case 2:
				System.out.println("Enter product id: ");
				String removeId = scanner.nextLine();
				
				System.out.println("Enter quantity to be removed: ");
				int removeQty = scanner.nextInt();
				scanner.nextLine();
				
				user.getCart().removeProduct(removeId, removeQty);
				break;
				
			case 3:
				user.getCart().displayCart();
				break;
				
			case 4: 
				double cost = user.getCart().calculateTotalCost();
				System.out.println("Total Amount to be paid: $" + cost);
				System.out.println("Thank you for shopping!!!");
				shopping = false;
				break;
				
			case 5: 
				shopping = false;
				break;
				
			default:
				System.out.println("Invalid choice. Please try again!!!");
			}
		}
		
		scanner.close();
	}
}
```
## How It Works:
* `Product Selection:` Users can browse available products from the shop's inventory. Each product has an ID, name, price, and available quantity.
* `Add to Cart:` Users can add products to their cart by specifying the product ID and quantity. The system checks if the product is already in the cart and adjusts the quantity accordingly.
* `Remove from Cart:` Users can remove products from the cart by product ID and quantity. If the quantity to remove exceeds the available quantity, the product is removed from the cart.
* `View Cart:` Users can view the items in their cart at any time, including the name, price, and quantity of each item.
* `Checkout:` The system calculates the total cost of all items in the cart and displays the final amount. The user can proceed to checkout or continue shopping.

## Extend the Project:
This is a basic implementation of an online shopping cart system. You can extend the project by adding the following features to make it more comprehensive and reliable:
* `User Authentication:` Implement login and signup functionality to manage different users.
* `Inventory Management:` Update product quantities in the inventory after each purchase and notify users if a product is out of stock.
* `Order History:` Track past purchases and display an order history to users.
* `Discounts and Offers:` Add functionality to apply discount codes or special offers during checkout.
* `Database Integration:` Connect the project to a database (e.g., MySQL, PostgreSQL) to persist product and user data.

## Conclusion
This **Online Shopping Cart System** provides a hands-on demonstration of how to use OOP concepts in Java to build a functional project. It’s an excellent foundation for learning the basics of object-oriented programming and can serve as a starting point for more advanced e-commerce systems.

Feel free to experiment and enhance this project with the features mentioned above or any other ideas you come up with. The sky’s the limit!