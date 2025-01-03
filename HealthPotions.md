
# Potion and Player Management System

## Object Oriented Design
In this project, Object-Oriented Design (OOD) is used to structure the game logic into separate classes such as Potion and Player, each containing relevant attributes and methods. This approach promotes modularity, reusability, and easier maintenance by focusing on how objects interact with each other to manage healing and mana restoration within the game.

### 1. **Potion Class Definition**

```c++
// Potion class to represent health and mana potions
class Potion {
public:
    int points;   // Healing or Mana points provided by the potion
    int quantity; // Number of available potions

    // Constructor to initialize potion points and quantity
    Potion(int p, int q) : points(p), quantity(q) {}
};
```

**Explanation:**
- The `Potion` class represents a potion's properties: how many points of health or mana it restores and how many of that potion are available.
- The constructor initializes the potion’s point value and its quantity.

---

### 2. **Player Class Definition**

```c++
// Player class to represent each player in the game
class Player {
private:
    std::string name;       // Player's name
    int currentHealth;      // Current health of the player
    int maxHealth;          // Maximum health of the player
    int currentMana;        // Current mana of the player
    int maxMana;            // Maximum mana of the player

public:
    // Constructor to initialize player attributes
    Player(std::string n, int ch, int mh, int cm, int mm) 
        : name(n), currentHealth(ch), maxHealth(mh), 
          currentMana(cm), maxMana(mm) {}

    // Heal the player by a certain amount
    void heal(int amount) {
        currentHealth += amount; // Increase current health by the heal amount
        if (currentHealth > maxHealth) {
            currentHealth = maxHealth;  // Cap health at maximum
        }
    }

    // Restore mana for the player
    void restoreMana(int amount) {
        currentMana += amount; // Increase current mana by the restore amount
        if (currentMana > maxMana) {
            currentMana = maxMana;  // Cap mana at maximum
        }
    }

    // Display player's current status
    void displayStatus() const {
        std::cout << name << " | Health: " << currentHealth << "/" << maxHealth 
                  << " | Mana: " << currentMana << "/" << maxMana << std::endl;
    }
};
```

**Explanation:**
- The `Player` class encapsulates a player's attributes, including their name, current health and mana, and maximum health and mana.
- The constructor initializes these attributes.
- Methods include:
  - `heal(int amount)`: Increases the player's health and caps it at the maximum.
  - `restoreMana(int amount)`: Increases the player's mana and caps it at the maximum.
  - `displayStatus()`: Prints the player's current health and mana.

---

### 3. **Potion Log Display Function**

```c++
// Function to display the remaining potions
void displayPotionLog(const std::vector<Potion>& potions, const std::string& type) {
    std::cout << "=== " << type << " Potions ===" << std::endl; // Title for potion type
    std::cout << type + " Points | Quantity" << std::endl; // Column headers
    std::cout << std::string(30, '-') << std::endl; // Separator line
    
    // Loop through each potion to display its points and quantity
    for (const auto& potion : potions) {
        std::cout << potion.points << "          | " << potion.quantity << std::endl;
    }
    std::cout << std::endl; // Extra line for spacing
}
```

**Explanation:**
- The `displayPotionLog` function outputs a formatted table of potion types, showing their points and quantities.
- It takes a vector of `Potion` objects and a string indicating the type of potions (e.g., "Health" or "Mana") as parameters.

---

### 4. **Heal Players Function**

```c++
// Function to heal players using the available potions
void healPlayers(std::vector<Player>& players, std::vector<Potion>& healthPotions, std::vector<Potion>& manaPotions) {
    // Sort health and mana potions by points in descending order
    std::sort(healthPotions.begin(), healthPotions.end(), [](const Potion& leftPotion, const Potion& rightPotion) {
        return leftPotion.points > rightPotion.points;
    });
    std::sort(manaPotions.begin(), manaPotions.end(), [](const Potion& leftPotion, const Potion& rightPotion) {
        return leftPotion.points > rightPotion.points;
    });

    // Loop through each player to heal and restore mana
    for (auto& player : players) {
        player.displayStatus(); // Display player's status before healing
        int requiredHealAmount = player.getMaxHealth() - player.getCurrentHealth();
        
        // Loop through health potions to heal the player
        for (int i = 0; i < healthPotions.size(); ++i) {
            auto& potion = healthPotions[i];
            if (potion.quantity <= 0) continue; // Skip if no potions left
            if (requiredHealAmount >= potion.points) {
                requiredHealAmount -= potion.points; // Decrease required heal amount
                player.heal(potion.points); // Heal player
                potion.quantity--; // Decrease potion quantity
                i = -1; // Restart loop to check potions again
            }
        }

        // Similar logic for mana restoration
        int requiredManaAmount = player.getMaxMana() - player.getCurrentMana();
        for (int i = 0; i < manaPotions.size(); ++i) {
            auto& potion = manaPotions[i];
            if (potion.quantity <= 0) continue; // Skip if no potions left
            if (requiredManaAmount >= potion.points) {
                requiredManaAmount -= potion.points; // Decrease required mana amount
                player.restoreMana(potion.points); // Restore mana
                potion.quantity--; // Decrease potion quantity
                i = -1; // Restart loop to check potions again
            }
        }

        // Display updated status
        std::cout << "-----------------------------------------\n";
        player.displayStatus(); // Show player's status after healing
    }
}
```

**Explanation:**
- The `healPlayers` function manages the healing and mana restoration process for each player.
- It sorts health and mana potions by their effectiveness (points) in descending order.
- after user testing and editing the code based on input i found that reorganising the array for the potions broke the code and had to fix that
- It iterates through each player, checking their health and mana requirements, and applies potions as necessary, updating the quantities accordingly.

---

### 5. **Main Function**

```c++
int main() {
    // Initialize players
    std::vector<Player> players = { 
        {"Mage", 90, 100, 30, 60},
        {"Knight", 70, 100, 40, 80},
        {"Rogue", 65, 100, 20, 50},
        {"Cleric", 85, 100, 50, 90}
    };

    // Initialize health and mana potions
    std::vector<Potion> healthPotions = { {50, 3}, {20, 5}, {10, 4} };
    std::vector<Potion> manaPotions = { {30, 2}, {15, 4}, {5, 2} };

    healPlayers(players, healthPotions, manaPotions); // Heal players
    return 0; // End of the program
}
```

## Explanation
- The `main` function serves as the entry point of the program.
- It initializes a list of players with their respective health and mana attributes.
- It also initializes available health and mana potions.
- Finally, it calls the `healPlayers` function to apply the potions to the players.
Got it! Here’s a cheat sheet formatted in a table with explanations for the Potion and Player Management System, structured like the previous one you provided.

---
## learning
This task was enjoyable and engaging. While dual coding was challenging at times, it provided a valuable learning experience. Having two people working together made it easier to catch mistakes and test thoroughly. To improve the user experience and add more complexity, I also included a log system. i also added a mana system to try and complicate the system and test if it would break with multiple things to track.

## Improvement
An improvement could be to add a cooldown system for potions, so they can’t be used repeatedly in quick succession. Another idea would be to implement potion crafting, where players can combine ingredients to create custom potions. i could implement this along with an inventory system to make a more fleshed out gameplay interaction like a DND textgame.
## Cheat Sheet

| **Code**                           | **Description**                                                      |
|:-----------------------------------|:---------------------------------------------------------------------|
| `class Potion`                     | Represents a potion with healing or mana points.                    |
| `int points`                       | Healing or mana points provided by the potion.                      |
| `int quantity`                     | Number of available potions.                                        |
| `Potion(int p, int q)`             | Constructor to initialize potion points and quantity.               |
| `class Player`                     | Represents a player with health and mana attributes.                |
| `std::string name`                | Player's name.                                                      |
| `int currentHealth`                | Current health of the player.                                       |
| `int maxHealth`                    | Maximum health of the player.                                       |
| `int currentMana`                  | Current mana of the player.                                         |
| `int maxMana`                      | Maximum mana of the player.                                         |
| `Player(std::string n, int ch, int mh, int cm, int mm)` | Constructor to initialize player attributes.               |
| `void heal(int amount)`            | Increases the player's current health, capped at maximum health.    |
| `void restoreMana(int amount)`     | Increases the player's current mana, capped at maximum mana.        |
| `bool needsHealing() const`        | Returns true if the player needs healing (current health < max health). |
| `bool needsMana() const`           | Returns true if the player needs mana (current mana < max mana).   |
| `void displayStatus() const`       | Displays the player's current health and mana status.               |
| `void displayPotionLog(...)`       | Displays the available potions with points and quantities.          |
| `void healPlayers(...)`            | Heals players and restores mana using available potions.            |
| `std::vector<Potion>`              | Stores multiple Potion objects.                                     |
| `std::vector<Player>`              | Stores multiple Player objects.                                     |
| `std::sort(...)`                   | Sorts the potions based on points in descending order.             |
| `potion.quantity--`                | Decreases the quantity of the potion used by one.                   |
--- 
bibliography:

[chatgpt](https://chatgpt.com/)

[geeksforgeeks](https://www.geeksforgeeks.org/introduction-of-object-oriented-programming/)

[nexwebsities](https://nexwebsites.com/blog/object-oriented-design-with-cpp/)

Declared Asssets:

[chatgpt4.0](https://chatgpt.com/) (HealthPotions.md)
