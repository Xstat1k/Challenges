# Charactor Creator Challenge

This part of the project focuses on creating characters with predefined stats based on their chosen class. The system uses a `Character` class to hold the basic attributes and a `CharacterFactory` to generate characters with appropriate stats.

---

## **1. Character Base Class**

```cpp
class Character
{
public:
    std::string name;
    CharacterClass characterClass;
    int strength, agility, endurance, intelligence, willpower, speed, luck;

    Character(std::string n, CharacterClass c)
        : name(n), characterClass(c), strength(5), agility(5), endurance(5),
        intelligence(5), willpower(5), speed(5), luck(5) {}

    virtual void PrintCharacterInfo() {
        std::cout << "Name: " << name << ", Class: " << toString(characterClass) << std::endl;
        std::cout << "Strength: " << strength << ", Agility: " << agility
                  << ", Endurance: " << endurance << ", Intelligence: " << intelligence
                  << ", Willpower: " << willpower << ", Speed: " << speed
                  << ", Luck: " << luck << std::endl;
    }

    virtual ~Character() = default;
};
```
- The `Character` class represents a character's basic properties, including its name, class, and attributes like strength, agility, and intelligence.
- It has a constructor that initializes default values for each attribute (set to 5) and a `PrintCharacterInfo` method to display the character's details.
- Example: A `Character` object named "John" can have its attributes like strength and agility printed when calling `PrintCharacterInfo()`.

---

## **2. Character Factory**

```cpp
class CharacterFactory
{
private:
    static const std::map<CharacterClass, std::vector<int>> classStats;

public:
    static Character* CreateCharacter(const std::string& name, CharacterClass charClass)
    {
        // Check if the class exists in the map
        auto it = classStats.find(charClass);
        if (it == classStats.end()) {
            std::cout << "Invalid character class!" << std::endl;
            return nullptr;
        }

        // Create the character and set the stats
        Character* character = new Character(name, charClass);
        const std::vector<int>& stats = it->second;

        character->strength = stats[0];
        character->agility = stats[1];
        character->endurance = stats[2];
        character->intelligence = stats[3];
        character->willpower = stats[4];
        character->speed = stats[5];
        character->luck = stats[6];

        return character;
    }
};
```
- The `CharacterFactory` is responsible for creating characters with specific stats based on their class.
- It uses a static map (`classStats`) that stores the attribute values for each class. When a character is created, their stats are initialized based on their class.
- Example: If a `Warrior` class is selected, the factory will assign higher strength and endurance values to the character.

---

## **3. Main Function for Character Creation**

```cpp
int main()
{
    // Prompt user for character name
    std::string name;
    std::cout << "Enter character name: ";
    std::getline(std::cin, name);

    // Prompt user to choose a character class
    std::cout << "Choose a character class:\n";
    std::cout << "1. Warrior\n2. Rogue\n3. Mage\n4. Wizard\n5. Ranger\n6. Monk\n7. Bard\n8. Paladin\n9. Cleric\n";
    int choice;
    std::cout << "Enter the number for the class: ";
    std::cin >> choice;
}
```
- The `main` function prompts the user to enter a name and select a character class by entering a number.
- It allows the user to customize their character by choosing one of the predefined classes and then calling the `CharacterFactory` to create a character with that class.
- Example: If the user enters `1`, it selects the `Warrior` class for the new character, which then gets created with the appropriate stats.

---

## Item Equipment
```cpp
    // Decorate character with chosen equipment
    if (equipChoice == 1) {
        character = new EnchantedArmorDecorator(character);
    } else if (equipChoice == 2) {
        character = new SpecialWeaponDecorator(character);
    }
```
- here there are preset items for the player to chose from

  ## Learning
This was another dual coding project and was very engaging and fun. It was challenging understanding the process of factories and decorators, especially figuring out how to create objects dynamically with the Factory pattern and how to add new features to them without modifying their original code using the Decorator pattern. Despite the challenges, it was rewarding to see how these patterns made the code more flexible and easier to maintain.

## improvements 
in future i would of liked to add more ustomisation on the charactor creator such as more/ multipke items that can be quipped or allow the user to add custom ones.


