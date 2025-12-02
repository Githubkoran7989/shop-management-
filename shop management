#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#define MAX_PRODUCTS 50
#define MAX_CART_ITEMS 100

// Safe integer input
int safe_int_input() {
    int num;
    while (scanf("%d", &num) != 1) {
        printf("Invalid input! Enter only numbers: ");
        while (getchar() != '\n'); // Clear buffer
    }
    return num;
}

// Product structure
struct Product {
    int id;
    char name[50];
    float price;
    int quantity;
};

// Cart item structure
struct CartItem {
    int product_id;
    int quantity;
    float total_price;
};

struct Product products[MAX_PRODUCTS];
struct CartItem cart[MAX_CART_ITEMS];
int product_count = 0;
int cart_count = 0;

// Initialize 8 products
void initialize_products() {
    product_count = 8;

    strcpy(products[0].name, "Laptop");      products[0].id = 1; products[0].price = 45000; products[0].quantity = 10;
    strcpy(products[1].name, "Mouse");       products[1].id = 2; products[1].price = 500;   products[1].quantity = 50;
    strcpy(products[2].name, "Keyboard");    products[2].id = 3; products[2].price = 1500;  products[2].quantity = 30;
    strcpy(products[3].name, "Monitor");     products[3].id = 4; products[3].price = 12000; products[3].quantity = 15;
    strcpy(products[4].name, "USB Cable");   products[4].id = 5; products[4].price = 200;   products[4].quantity = 100;
    strcpy(products[5].name, "Headphones");  products[5].id = 6; products[5].price = 2000;  products[5].quantity = 25;
    strcpy(products[6].name, "Webcam");      products[6].id = 7; products[6].price = 3000;  products[6].quantity = 20;
    strcpy(products[7].name, "Desk Lamp");   products[7].id = 8; products[7].price = 800;   products[7].quantity = 40;
}

// Display all products
void display_products() {
    printf("\nID   Product Name         Price     Stock\n");
    printf("----------------------------------------\n");
    for(int i = 0; i < product_count; i++) {
        printf("%-4d %-20s Rs.%-8.2f %-5d\n",
               products[i].id, products[i].name, products[i].price, products[i].quantity);
    }
}

// Find product index by ID
int find_product(int id) {
    for(int i = 0; i < product_count; i++) {
        if(products[i].id == id) return i;
    }
    return -1;
}

// Add product to cart
void add_to_cart() {
    int product_id, qty;
    int product_index;
    int add_more = 1;

    while(add_more) {
        display_products();
        printf("\nEnter Product ID: ");
        product_id = safe_int_input();

        product_index = find_product(product_id);
        if(product_index == -1) {
            printf("Product not found!\n");
            continue;
        }

        printf("Enter Quantity: ");
        qty = safe_int_input();

        if(qty <= 0 || qty > products[product_index].quantity) {
            printf("Invalid or insufficient stock! Available: %d\n", products[product_index].quantity);
            continue;
        }

        cart[cart_count].product_id = product_id;
        cart[cart_count].quantity = qty;
        cart[cart_count].total_price = products[product_index].price * qty;
        cart_count++;

        printf("Product added to cart successfully!\n");

        printf("Add another product? (1 = Yes, 0 = No): ");
        add_more = safe_int_input();
    }
}

// View cart
void view_cart() {
    if(cart_count == 0) {
        printf("\nCart is empty!\n");
        return;
    }

    float subtotal = 0;
    printf("\nID   Product Name         Qty   Price     Total\n");
    printf("------------------------------------------------\n");

    for(int i = 0; i < cart_count; i++) {
        int index = find_product(cart[i].product_id);
        printf("%-4d %-20s %-5d Rs.%-8.2f Rs.%-8.2f\n",
               cart[i].product_id, products[index].name, cart[i].quantity,
               products[index].price, cart[i].total_price);
        subtotal += cart[i].total_price;
    }
    printf("------------------------------------------------\n");
    printf("Subtotal: Rs.%.2f\n", subtotal);
}

// Remove item from cart
void remove_from_cart() {
    if(cart_count == 0) {
        printf("\nCart is empty!\n");
        return;
    }

    view_cart();
    printf("\nEnter cart item number to remove (1-%d): ", cart_count);
    int index = safe_int_input();

    if(index < 1 || index > cart_count) {
        printf("Invalid index!\n");
        return;
    }

    for(int i = index - 1; i < cart_count - 1; i++) {
        cart[i] = cart[i + 1];
    }
    cart_count--;
    printf("Item removed successfully!\n");
}

// Generate bill
void generate_bill() {
    if(cart_count == 0) {
        printf("\nCart is empty!\n");
        return;
    }

    float subtotal = 0, tax, total;
    time_t now = time(NULL);
    struct tm *timeinfo = localtime(&now);

    printf("\n================= BILL =================\n");
    printf("Date: %s", asctime(timeinfo));
    printf("ID   Product Name         Qty   Price     Total\n");
    printf("---------------------------------------------\n");

    for(int i = 0; i < cart_count; i++) {
        int index = find_product(cart[i].product_id);
        printf("%-4d %-20s %-5d Rs.%-8.2f Rs.%-8.2f\n",
               cart[i].product_id, products[index].name, cart[i].quantity,
               products[index].price, cart[i].total_price);
        subtotal += cart[i].total_price;
        products[index].quantity -= cart[i].quantity;
    }

    tax = subtotal * 0.05;
    total = subtotal + tax;

    printf("---------------------------------------------\n");
    printf("Subtotal: Rs.%.2f\n", subtotal);
    printf("Tax (5%%): Rs.%.2f\n", tax);
    printf("TOTAL: Rs.%.2f\n", total);
    printf("============================================\n");

    cart_count = 0;
}

// Main function
int main() {
    int choice;
    initialize_products();

    while(1) {
        printf("\n========= SHOP MENU =========\n");
        printf("1. View Products\n");
        printf("2. Add to Cart\n");
        printf("3. View Cart\n");
        printf("4. Remove from Cart\n");
        printf("5. Generate Bill\n");
        printf("6. Exit\n");
        printf("==============================\n");
        printf("Enter choice: ");

        choice = safe_int_input();

        switch(choice) {
            case 1: display_products(); break;
            case 2: add_to_cart(); break;
            case 3: view_cart(); break;
            case 4: remove_from_cart(); break;
            case 5: generate_bill(); break;
            case 6: printf("Exiting program...\n"); exit(0);
            default: printf("Invalid choice!\n");
        }
    }
    return 0;
}
