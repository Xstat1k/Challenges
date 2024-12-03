# Data Driven Movement

This project implements a simple movement system using Data-Oriented Design (DOD). In DOD, we focus on organizing data efficiently and separating it from the behavior (logic). The goal is to handle data in a way that maximizes performance, especially when dealing with large numbers of entities, like players or enemies.


```cpp
struct EntityData
{
    float positionX;
    float positionY;
    float positionZ;
    float velocityX;
    float velocityY;
    float velocityZ;

    EntityData(float posX, float posY, float posZ, float velX, float velY, float velZ)
        : positionX(posX), positionY(posY), positionZ(posZ), velocityX(velX), velocityY(velY), velocityZ(velZ) {}
};
```

The EntityData struct stores the position and velocity of each entity (e.g., player or enemy). This structure allows us to keep all the necessary information in one place for each entity. We are not using any complex classes or behaviors here—just simple data that can be processed efficiently.


```cpp
class MovementSystem
{
public:
    std::vector<EntityData> entities;  // Store all entities' data

    void UpdatePositions(float deltaTime);  // Function to update positions based on velocity
    void PrintPositions();  // Function to print positions of all entities
};
```
The MovementSystem class holds all the entities in a std::vector. It has two main functions:
UpdatePositions(float deltaTime): Updates the position of all entities based on their velocity and the time passed (deltaTime). PrintPositions(): Prints the current positions of all entities for debugging.
This class shows how DOD focuses on handling the data (the entities) separately from the logic (how the positions are updated).

```cpp
void MovementSystem::UpdatePositions(float deltaTime)
{
    for (auto& entity : entities)  // Loop through all entities
    {
        entity.positionX += entity.velocityX * deltaTime;  // Update X position
        entity.positionY += entity.velocityY * deltaTime;  // Update Y position
        entity.positionZ += entity.velocityZ * deltaTime;  // Update Z position
    }
}
```

In this function, we loop through each entity and update its position based on its velocity. The position is updated by multiplying the velocity by the time step (deltaTime). This is a simple and efficient way to move the entities forward based on their speed. This is an example of how DOD works: the data is updated in a straightforward loop, and all entities are processed together.

```cpp
void MovementSystem::PrintPositions()
{
    for (const auto& entity : entities)
    {
        std::cout << "Entity Position: X=" << entity.positionX << ", Y=" << entity.positionY
                  << ", Z=" << entity.positionZ << std::endl;
    }
}
```
This function prints the position of each entity. It helps us see how the entities' positions change over time. Printing the data is a simple operation that doesn’t involve complex logic, which is in line with the DOD principle of focusing on data first.


```cpp
int main()
{
    MovementSystem movementSystem;

    // Adding entities with initial positions and velocities
    movementSystem.entities.push_back(EntityData(0, 0, 0, 1, 0, 0));  // Entity 1
    movementSystem.entities.push_back(EntityData(1, 2, 3, 0, 1, 0));  // Entity 2
    movementSystem.entities.push_back(EntityData(5, 5, 5, 0, 0, 1));  // Entity 3

    // Simulate movement over multiple frames
    for (int frame = 0; frame < 5; frame++)
    {
        std::cout << "\nFrame " << frame + 1 << std::endl;
        movementSystem.PrintPositions();    // Print current positions
        movementSystem.UpdatePositions(0.016f);  // Update positions (16ms per frame)
    }

    return 0;
}
```
In the main function:
We create a MovementSystem object.
We add a few entities with initial positions and velocities.
We run a loop for 5 frames, printing the positions of all entities and updating their positions based on their velocity each time. This part shows how the movement system works in action: every frame, we update and print the positions, allowing us to observe how the entities move.

# Learning

Through implementing Data-Oriented Design for the movement system, I learned how separating data from logic improves performance and scalability. By storing data in simple structs and processing it in batches, the system became more efficient, especially when handling multiple entities. This approach simplified the movement logic and made it easier to focus on performance, demonstrating the benefits of DOD in handling large-scale data efficiently.

# Improvement

If I worked on this project more, I could improve the movement system by adding more detailed behaviors, like rotating entities or changing their velocity over time. I could also make the code more flexible by allowing different movement patterns, like diagonal movement or gravity. Another improvement could be to better handle edge cases, such as entities moving off-screen or ensuring the system can scale for more entities.

| **Function**               | **Description**                                                                                                                                     |
|----------------------------|----------------------------------------------|
| `EntityData(float, float, float, float, float, float)` | Constructor to initialize an entity's position and velocity with the provided values.|
| `void UpdatePositions(float deltaTime)` | Updates the positions of all entities based on their velocity and the given `deltaTime`.                                                 |
| `void PrintPositions()`      | Prints the current positions (X, Y, Z) of all entities stored in the `entities` vector.                                                          |
| `main()`                    | Initializes the `MovementSystem`, adds entities to it, and simulates multiple frames while updating and printing entity positions.                  |
