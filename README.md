#include <iostream>
#include <map>
#include <vector>
#include <algorithm>

using namespace std;

// Define a structure for a food item
struct FoodItem {
    string name;
    int quantity;
};

// Function to add a food item to the inventory
void addFoodItem(map<string, int>& inventory) {
    string name;
    int quantity;
    cout << "Enter the name of the food item: ";
    cin >> name;
    cout << "Enter the quantity: ";
    cin >> quantity;
    inventory[name] += quantity;
    cout << "Food item added to inventory." << endl;
}

// Function to remove a food item from the inventory
void removeFoodItem(map<string, int>& inventory) {
    string name;
    int quantity;
    cout << "Enter the name of the food item you want to remove: ";
    cin >> name;
    cout << "Enter the quantity to remove: ";
    cin >> quantity;
    if (inventory.find(name) != inventory.end() && inventory[name] >= quantity) {
        inventory[name] -= quantity;
        cout << "Food item removed from inventory." << endl;
    } else {
        cout << "Error: Item not found or quantity exceeds available amount." << endl;
    }
}

// Function to display the current inventory
void displayInventory(const map<string, int>& inventory) {
    cout << "Current Inventory:" << endl;
    for (const auto& item : inventory) {
        cout << "- " << item.first << ": " << item.second << " units" << endl;
    }
}

// Function to suggest recipes based on available ingredients
void suggestRecipes(const map<string, int>& inventory) {
    // Example recipes
    map<string, vector<string>> recipes = {
        {"Pasta", {"Pasta", "Tomato", "Garlic", "Olive oil"}},
        {"Sandwich", {"Bread", "Cheese", "Tomato", "Lettuce"}}
    };

    cout << "Available recipes:" << endl;
    for (const auto& recipe : recipes) {
        bool canMake = true;
        for (const auto& ingredient : recipe.second) {
            if (inventory.find(ingredient) == inventory.end() || inventory.at(ingredient) <= 0) {
                canMake = false;
                break;
            }
        }
        if (canMake) {
            cout << "- " << recipe.first << endl;
        }
    }
}

int main() {
    map<string, int> inventory;

    // Sample inventory initialization
    inventory["Tomato"] = 3;
    inventory["Pasta"] = 1;
    inventory["Garlic"] = 2;

    int choice;
    do {
        cout << "\nPlate Pledge Food Wastage Reduction App\nMenu:\n1. Add Food Item\n2. Remove Food Item\n3. Display Inventory\n4. Get Recipe Suggestions\n5. Exit\nEnter your choice: ";
        cin >> choice;
        switch (choice) {
            case 1:
                addFoodItem(inventory);
                break;
            case 2:
                removeFoodItem(inventory);
                break;
            case 3:
                displayInventory(inventory);
                break;
            case 4:
                suggestRecipes(inventory);
                break;
            case 5:
                cout << "Exiting...";
                break;
            default:
                cout << "Invalid choice. Please try again.";
        }
    } while (choice != 5);

    return 0;
}
