# Inventory Code Challenge!

## What is bubble sort?

Bubble sort is an algorithm that works by comparing two numbers in a data set and comparing them, the larger numbers are moved to the top (like large bubbles floating up), this is repeated in a loop untill all numbers have been sorted.while useful for small data sets it is ineffeicent with large ones.

### *bubbble sort template (c++)*
```c++
void BubbleSort(std::vector<Item>& items, bool (*compare)(const Item&, const Item&))  
{ 
    for (size_t i = 0; i < items.size() - 1; i++) 
    { 
        for (size_t j = 0; j < items.size() - 1 - i; j++) 
        { 
            if (compare(items[j], items[j + 1]))  
            { 
                std::swap(items[j], items[j + 1]); 
            } 
        } 
    } 
}
```

The `BubbleSort` function sorts a vector of `Item` objects by comparing adjacent items and swapping them based on a provided comparison function. The outer loop, controlled by **`i`**, runs **`n-1`** times (where **`n`** is the vector size), while the inner loop, controlled by **`j`**, iterates from the start to **`n-1-i`** to avoid redundant comparisons, effectively "bubbling" larger items to the end of the vector. This process continues until the entire vector is sorted.
By using this method i can call a switch case function to organinse based on existing variables whie leaving the option to easily add new ones.


```c++
bool CompareByNameAscending(const Item& a, const Item& b)  
{ 
    return a.Name > b.Name; 
} 
bool CompareByNameDescending(const Item& a, const Item& b) 
{ 
    return a.Name < b.Name; 
} 
bool CompareByValueAscending(const Item& a, const Item& b) 
{ 
    return a.Value > b.Value; 
} 
bool CompareByValueDescending(const Item& a, const Item& b) 
{ 
    return a.Value < b.Value; 
} 
bool CompareByWeightAscending(const Item& a, const Item& b)  
{ 
    return a.Weight < b.Weight;  
} 
bool CompareByWeightDescending(const Item& a, const Item& b)  
{ 
    return a.Weight > b.Weight;  
} 
void SortItems(std::vector<Item>& items)  
{ 
    std::cout << "\nHow would you like to sort the items?\n"; 
    std::cout << "1. By Name(A-Z)\n2. By Name(Z-A)\n3. By Value(↓)\n4. By Value(↑)\n5. By Weight(↑)\n6. By Weight(↓)\n"; 
    std::cout << "Please enter choice(1-6): "; 
    int choice; 
    std::cin >> choice; 
    switch (choice)  
    { 
        case 1: BubbleSort(items, CompareByNameAscending); break; 
        case 2: BubbleSort(items, CompareByNameDescending); break; 
        case 3: BubbleSort(items, CompareByValueAscending); break; 
        case 4: BubbleSort(items, CompareByValueDescending); break; 
        case 5: BubbleSort(items, CompareByWeightAscending); break;  
        case 6: BubbleSort(items, CompareByWeightDescending); break;  
        default:  
            std::cout << "Invalid choice.\n";  
            return; 
    }
```
To test this i included a `weight` variable, to include this i had to define `weight int` and include it in the switch case. There was some issue with the code reading the `weight` int but that was mostly due to poor naming conventions.

## User Input

 I wanted to see how the code handled adding additional input so i included a simple interface that asks the user if they would like to add their own item.

 ```c++
std::string name; 
    int value, weight; 
    std::cout << "Enter the item name: "; 
    std::cin >> name; 
    std::cout << "Enter the item value: "; 
    if (std::cin >> value)  
    { 
        std::cout << "Enter the item weight: "; 
        if (std::cin >> weight)  
        { 
            items.emplace_back(name, value, weight); 
            std::cout << "Item '" << name << "' with value " << value << " and weight " << weight << " added.\n"; 
        }  
```
Here it asks the user to include the Name, Value and Weight of their own objects. By using the `emplace_back` function to temporarily add it into the Data list, i could have used the `push_back` function but i would also have to create a temporary object myself and add it to the vector. `Cout` handles displaying text and `Cin` handles user input. if the user tries to include something that cannot be handled it is rejected.









## Code Cheat Sheet
some code that was used and a simple descripton for future reference
|**Code**|**Description**|    
|:------------:|:------------:|
| *BubbleSort* | Defines function |
| *&* | memory reference to objects |
| *Item* |   Data type to be sorted |
| *Const* | Prevents Compare function from changing Item data |
| *size* | Holds positive interger data |
| *i* | Outer loop |
| *j* | Inner loop |
| *Compare* | Compares Item data|
| *Swap* | Swaps Item data|
| *Cout* | Character out|
| *Cin* | Character input |
| *Emplace_back* | adds temporary new data to the list|




bibliography:

[chatgpt](https://chatgpt.com/)

[wikipedia](https://en.wikipedia.org/wiki/Bubble_sort)

Declared Asssets:

[chatgpt4.0](https://chatgpt.com/) (InventoryMarkdown.md)
