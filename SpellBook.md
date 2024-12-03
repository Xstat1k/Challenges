
# Spell Inventory System

## Spell Inventory Overview

In this project, I used a hashmap to store spells and make searching more efficient. A hashmap maps each spell's name (the key) to its data (the value), allowing for quick lookups. This makes it faster to find a spell compared to searching through a list, as the hashmap provides near-instant access to any spell by its name.

### *Spell System Code (C++)*

```c++
// Define the target types for spells
enum class TargetType
{
    SingleTarget, // A spell that targets a single entity
    AOE,          // Area of Effect spell that affects multiple targets
    Self          // A spell that affects the caster
};

// Define the spell types
enum class SpellType
{
    Damage, // A spell that deals damage
    Heal,   // A spell that restores health
    Buff,   // A spell that enhances a target's abilities
    Debuff  // A spell that weakens a target's abilities
};


// The Spell class represents a single spell with its attributes
class Spell
{
public:
    std::string name;       // The name of the spell
    int manaCost;           // The mana cost to cast the spell
    int power;              // The power of the spell (effect strength)
    TargetType target;      // The type of target the spell can affect
    SpellType type;         // The type of spell (Damage, Heal, etc.)


    // Default constructor
    Spell() : name(""), manaCost(0), power(0), target(TargetType::SingleTarget), type(SpellType::Damage) {}

    // Constructor to initialize a Spell object
    Spell(std::string n, int mCost, int p, TargetType t, SpellType st)
        : name(n), manaCost(mCost), power(p), target(t), type(st) {}
```

This code categorizes spells, allowing users to pick spells based on their effect, mana cost, and target type. The TargetType enum defines if a spell targets a single entity, an area, or the caster, while the SpellType enum classifies spells as damage, healing, buffs, or debuffs. The Spell class stores each spell's attributes, helping manage them in the inventory.
   
```c++
// Function to create a list of spells
std::vector<Spell> CreateSpells()

// Function to create a hash map for spells based on their names
std::unordered_map<std::string, Spell> CreateSpellMap(const std::vector<Spell>& spellList)
{
    std::unordered_map<std::string, Spell> spellMap;
    for (const auto& spell : spellList)
    {
        spellMap[spell.name] = spell; // Store spell using its name as the key
    }
    return spellMap;
}

// Function to search for spells based on a keyword
void SearchSpells(const std::unordered_map<std::string, Spell>& spellMap, const std::string& keyword)
{
    bool found = false; // Flag to check if any spells matched the search
    for (const auto& pair : spellMap)
    {
        const Spell& spell = pair.second;
        // Check if the keyword matches any of the spell's properties
        if (spell.name.find(keyword) != std::string::npos ||
            spell.GetTargetTypeAsString().find(keyword) != std::string::npos ||
            spell.GetSpellTypeAsString().find(keyword) != std::string::npos)
        {
            spell.PrintSpell(); // Print the matching spell details
            found = true; // Mark that a match was found
        }
    }

    if (!found) // If no matches

 were found
    {
        std::cout << "No spells matched the search criteria." << std::endl; // Notify the user
    }
}

int main()
{
    std::vector<Spell> spells = CreateSpells(); // Create a list of spells
    auto spellMap = CreateSpellMap(spells); // Create a hash map of spells

    std::string keyword;
    std::cout << "Search terms: Damage, Heal, Buff, Debuff, SingleTarget, AOE, Self" << std::endl;
    std::cout << "Enter a search keyword:" << std::endl;

    while (std::getline(std::cin, keyword)) // Loop to continuously take user input
    {
        // Check for an exit command
        if (keyword == "exit")
        {
            break; // Exit the loop if the user types 'exit'
        }
        // Search for spells based on the keyword
        SearchSpells(spellMap, keyword);
        std::cout << "\nEnter another search keyword (or type 'exit' to quit):" << std::endl; // Prompt again
    }
    return 0; // Exit the program
}
```

This section includes functions for creating a list of spells, mapping them into a hash map for faster search, and enabling the search functionality. The CreateSpells function generates a list of predefined spells, while CreateSpellMap maps each spell's name to its corresponding object. The SearchSpells function allows users to search for spells using keywords, showing details of any matches found, and keeps prompting for new keywords until the user types "exit."

---
# Learning

This project gave me a hands-on understanding of how hashmaps work by mapping each spell's name to its data, making it easier and faster to search for spells. It was a great way to learn how hashmaps optimize data retrieval, and I look forward to using them again in future projects for efficient data management.

## Cheat Sheet

| **Code**                  | **Description**                                                   |
|:--------------------------|:------------------------------------------------------------------|
| *enum class TargetType*   | Define spell target types (SingleTarget, AOE, Self).              |
| *enum class SpellType*    | Define spell effects (Damage, Heal, Buff, Debuff).                |
| *Spell*                   | Class to define spells with properties like name, manaCost, power.|
| *Spell() constructor*     | Default constructor initializing a basic Spell object.            |
| *Spell(n, mCost, p, t, st)* | Constructor to initialize a Spell with specific values.        |
| *PrintSpell()*            | Method to print spell details to console.                         |
| *GetTargetTypeAsString()* | Converts TargetType to a readable string.                         |
| *GetSpellTypeAsString()*  | Converts SpellType to a readable string.                          |
| *CreateSpells()*          | Creates a list of predefined spells and returns as vector.        |
| *std::vector<Spell>*      | Collection to store multiple Spell objects.                       |
| *CreateSpellMap()*        | Creates a hash map of spells for efficient search by name.        |
| *std::unordered_map*      | Hash map used to store spells by name for faster access.          |
| *SearchSpells()*          | Searches the spell map for a keyword and prints matches.          |
| *std::getline*            | Reads a full line of user input.                                  |
| *std::cout*               | Outputs text to the console.                                      |
| *std::cin*                | Reads input from the user.                                        |
| *keyword == "exit"*       | Checks if user typed "exit" to quit the program.

bibliography:

[chatgpt](https://chatgpt.com/)

[geeksforgeeks](https://www.geeksforgeeks.org/how-to-use-hashmap-in-cpp/)

Declared Asssets:

[chatgpt4.0](https://chatgpt.com/) (SpellBook.md)
