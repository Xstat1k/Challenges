# Dialogue System Overview

This C# program implements a simple dialogue system using a tree structure where each node represents a dialogue option. Users can navigate through the dialogue based on their choices, leading to different branches of conversation.

## *Dialogue System Code (C#)*

```csharp
using System;
using System.Collections.Generic;
// The DialogueNode class represents a single dialogue option in the tree
public class DialogueNode
{
    public string text; // The text of the dialogue node
    public List<DialogueNode> children; // List of child dialogue nodes
    public DialogueNode(string text)
    {
        this.text = text;
        this.children = new List<DialogueNode>(); // Initialize the children list
    }
}
```
### Explanation:
- **DialogueNode Class**: Represents each dialogue option. It has a `text` property for the dialogue text and a `children` list to hold subsequent dialogue options.

```csharp
// The DialogueSystem class represents the overall dialogue system
public class DialogueSystem
{
    public DialogueNode First; // Root node of the dialogue tree

    public void BuildDialogueTree()
    {
        // Build the dialogue tree structure here
        DialogueNode start = new DialogueNode("Hey, this is the start.");
        DialogueNode option1 = new DialogueNode("How are you?");
        DialogueNode option2 = new DialogueNode("What are you doing?");
        DialogueNode option3 = new DialogueNode("Tell me about the town.");
        DialogueNode option4 = new DialogueNode("Goodbye.");

        // Connecting nodes
        start.children.Add(option1);
        start.children.Add(option2);
        start.children.Add(option3);
        start.children.Add(option4);
        
        // Adding children to option1
        option1.children.Add(new DialogueNode("I'm fine, thanks!"));
        option1.children.Add(new DialogueNode("Not so great..."));

        // Adding children to option2
        option2.children.Add(new DialogueNode("Just working on a project."));
        option2.children.Add(new DialogueNode("Just hanging out."));

        // Adding children to option3
        DialogueNode townInfo = new DialogueNode("The town is beautiful, with a great park and lots of shops.");
        townInfo.children.Add(new DialogueNode("What about the park?"));
        townInfo.children.Add(new DialogueNode("Are there any good restaurants?"));

        option3.children.Add(townInfo);
        option3.children.Add(new DialogueNode("I don't know much about it."));

        // Adding more children to the townInfo node
        townInfo.children[0].children.Add(new DialogueNode("It's a great place to relax and enjoy nature."));
        townInfo.children[0].children.Add(new DialogueNode("I heard there's a lake nearby."));

        townInfo.children[1].children.Add(new DialogueNode("There's a fantastic Italian place downtown."));
        townInfo.children[1].children.Add(new DialogueNode("The cafe on Main Street is very popular."));

        // Setting the first node
        First = start; // Root node of the dialogue tree
    }
}
```
### Explanation:
- **DialogueSystem Class**: Manages the dialogue system.
  - **First**: The root node of the dialogue tree.
  - **BuildDialogueTree()**: Constructs the dialogue tree, defining the connections between nodes to establish the flow of conversation.

```csharp
    public DialogueNode ReadNode(DialogueNode currentNode)
    {
        Console.WriteLine($"{currentNode.text}"); // Display current node text
        Console.Write($"Choose an option: \n");

        for (int i = 0; i < currentNode.children.Count; i++)
        {
            Console.WriteLine($"{i + 1}: {currentNode.children[i].text}"); // Display options
        }

        string input = Console.ReadLine();
        int choice;

        bool correct = false;
        while (!correct)
        {
            if (int.TryParse(input, out choice) && choice > 0 && choice <= currentNode.children.Count)
            {
                currentNode = currentNode.children[choice - 1]; // Move to the chosen child
                correct = true; // Valid choice
            }
            else
            {
                Console.WriteLine("Invalid choice. Try again."); // Handle invalid input
                input = Console.ReadLine();
            }
        }
        if (currentNode.children.Count != 0)
            return ReadNode(currentNode); // Continue reading if there are more children
        return currentNode; // Return the current node if it's a leaf
    }
```
### Explanation:
- **ReadNode()**: Displays the current dialogue and prompts the user to choose an option.
  - Validates user input and navigates through the dialogue tree based on user choices.

```csharp
    public void StartDialogue()
    {
        DialogueNode a = ReadNode(First); // Start reading from the first node
        Console.WriteLine("You got to the end."); // Indicate end of dialogue
    }
}
```
### Explanation:
- **StartDialogue()**: Initiates the dialogue process by calling `ReadNode` starting from the first node and indicates when the dialogue ends.

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        DialogueSystem dialogueSystem = new DialogueSystem();

        dialogueSystem.BuildDialogueTree(); // Build the dialogue structure
        dialogueSystem.StartDialogue();     // Start navigating through the dialogue
    }
}
```
### Explanation:
- **Main()**: Entry point of the program that initializes the dialogue system, builds the tree, and starts the dialogue.
---
## Cheat Sheet
| **Code**                                         | **Description**                                                 |
|:-------------------------------------------------|:---------------------------------------------------------------|
| `class DialogueNode`                             | Represents a single dialogue option in the tree.              |
| `string text`                                   | Text displayed for the dialogue option.                       |
| `List<DialogueNode> children`                   | List of child nodes for branching dialogue options.           |
| `DialogueNode(string text)`                      | Constructor to initialize a dialogue node with text.          |
| `class DialogueSystem`                           | Manages the entire dialogue system.                           |
| `DialogueNode First`                             | Root node of the dialogue tree.                               |
| `void BuildDialogueTree()`                       | Constructs the dialogue structure and connections.            |
| `void ReadNode(DialogueNode currentNode)`       | Displays current node's text and options, navigates through choices. |
| `void StartDialogue()`                           | Starts the dialogue flow by invoking `ReadNode`.             |
| `public static void Main(string[] args)`        | Entry point of the program; initializes and starts the dialogue. |
| `Console.WriteLine()`                            | Outputs text to the console.                                  |
| `Console.ReadLine()`                            | Reads input from the user.                                   |
| `int.TryParse()`                                 | Tries to convert input to an integer and checks validity.    |

---

bibliography:

[chatgpt](https://chatgpt.com/)

[geeksforgeeks](https://www.geeksforgeeks.org/tree-data-structure/)

Declared Asssets:

[chatgpt4.0](https://chatgpt.com/) (DialougeTree.md)
