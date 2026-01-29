# ECS Breakout Game Engine

A complete Entity-Component-System (ECS) game engine implemented in JavaScript following strict functional programming principles. This project constructs a fully functional Breakout game demonstrating ECS architecture with immutable data structures, function composition, and higher-order functions.


## Project Overview

This implementation provides:

- Pure ECS architecture with entity-component separation
- Functional programming paradigm throughout (immutability, composition, higher-order functions)
- Mouse-only paddle control with smooth movement tracking
- Complete game lifecycle: start screen, active play, pause states, win/lose conditions
- 120 rainbow-colored bricks across 10 rows with progressive destruction
- Real-time scoring and lives management
- 60fps rendering with requestAnimationFrame


## Project Structure

ECS-Breakout/
├── index.html # Complete single-file implementation
├── README.md # This documentation
└── (No external dependencies)


## ECS Architecture

The system implements 6 core systems processing entities through a functional pipeline:

InputSystem -> PhysicsSystem -> CollisionSystem -> ScoreSystem -> LivesSystem -> RenderSystem

### Required Systems (Course Specification)

1. **InputSystem** - Mouse movement and keyboard input with priority logic
2. **RenderSystem** - Complete canvas rendering with game state UI

### Custom Student-Defined Systems

1. **PhysicsSystem** - Ball movement and boundary collision detection
2. **CollisionSystem** - Brick destruction and paddle collision response
3. **ScoreSystem** - Real-time brick destruction counting
4. **LivesSystem** - Win/lose conditions, life management, ball reset


## Functional Programming Principles

| Principle | Implementation |
|-----------|----------------|
| Function Composition | `pipe()` chains all game systems |
| Immutability | `updateEntity()` creates new entities |
| Higher-Order Functions | Systems as pure functions: `entities => entities` |
| Map/Filter/Reduce | Entity queries and transformations |


## Features

### Input Handling
- Primary: Mouse movement (smooth paddle tracking)
- Secondary: Arrow keys (overrides mouse when active)
- Start/Continue: Spacebar or mouse click
- Priority: Keys > Moving Mouse > Stationary

### Game Mechanics
- 120 bricks (12x10 grid) with row-based rainbow coloring
- Ball physics with wall bounce and velocity reflection
- Paddle collision with position correction
- Lives system (3 lives) with pause between losses
- Win condition: All bricks destroyed
- Lose condition: Ball falls below paddle with 0 lives

### Visual System
- Start screen with instructions
- Pause screen on life loss
- Active game with real-time HUD (score/lives)
- Brick rendering with gradient colors and borders
- Smooth 60fps animation loop


## Technical Implementation

### Core ECS Components

Position(x, y) // Spatial coordinates
Velocity(dx, dy) // Movement vector
Size(width, height) // Dimensions
Renderable(color) // Visual properties
InputControlled // Paddle marker
BrickData(status, row) // Brick state and position
ScoreData(value) // Current score
LivesData(value) // Remaining lives
GameStateData(...) // Game phase states

### Immutable Entity Updates
```javascript
const updateEntity = (entity, updates) => Object.assign(
    Object.create(Entity.prototype),
    { 
        id: entity.id,
        components: {
            ...entity.components,
            ...Object.fromEntries(/* spread merge */)
        }
    }
);

### System Pipeline Composition
```javascript
const gameSystems = pipe(
    PhysicsSystem,
    CollisionSystem, 
    ScoreSystem,
    LivesSystem
);


## Setup Instructions

### Prerequisites
- Modern web browser (Chrome, Firefox, Safari, Edge)
- No server or dependencies required

### Running the Game

1. Save the complete code as `index.html`

2. Open directly in any modern web browser:
file:///path/to/index.html

3. **Click or press SPACE** to start the game

4. **Move mouse** to control paddle (most responsive)

5. **Arrow keys** as keyboard alternative


## Game Controls

| Action | Primary Input | Secondary Input |
|--------|---------------|-----------------|
| Start/Resume | Mouse Click | Spacebar |
| Paddle Left/Right | Mouse Movement | Left/Right Arrows |
| Priority | Moving Mouse | Keyboard Keys |


## Performance Characteristics

- Canvas: 1280x720 pixels
- Frame Rate: 60fps via requestAnimationFrame
- Entities: ~125 (1 ball, 1 paddle, 120 bricks, 3 game state)
- Input Polling: 10ms mouse movement reset
- No garbage collection pauses (immutable updates)


## Course Requirements Compliance

**Constructed ECS engine for a videogame in JavaScript**: Complete Breakout implementation

**Functional paradigm**: 
- Pure function systems
- Immutable entity updates
- Function composition via pipe()
- Higher-order system functions
- map/filter/reduce for entity processing

**Required systems**:
- InputSystem (mouse + keyboard)
- RenderSystem (complete UI states)

**Student-defined systems (4)**:
- PhysicsSystem (ball movement)
- CollisionSystem (brick/paddle hits)
- ScoreSystem (destruction counting)
- LivesSystem (win/lose logic)


## Key Predefined Metrics

| Component   | Specification              |
| ----------- | -------------------------- |
| Bricks      | 120 (12 columns x 10 rows) |
| Lives       | 3                          |
| Paddle      | 150x15 pixels              |
| Ball        | 20px diameter, ±5 velocity |
| Performance | 60fps, no dependencies     |


## Extending the Engine

New systems integrate seamlessly (example):

```javascript
const PowerUpSystem = entities => {
 // Process power-ups
 return entities.map(updateEntity);
};

const extendedPipeline = pipe(gameSystems, PowerUpSystem);


## License

This project is licensed under the GNU GPL v3 License - see the LICENSE file for details.