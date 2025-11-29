# Game_of_life_variant

this is a new game created by deyang, oriented by convey's game of life. this game provides some more control for the user on the came, including to edit the grid at any time, to stop the simulation and to change the rules about survival and death of cells;
also, a fuction that allows the user to save and load current status is set up;

imported tools: numpy, pygame，os

GEN1 allows users to interact with the game using the keyboard, with simple display. 

explanation

## How the Code Works  

### 1. Core Setup  
- **Grid**: A 2D grid (rows × columns) where cells exist.  
- **Rules**:  
  - **Birth**: A dead cell becomes alive if it has exactly 3 live neighbors.  
  - **Survival**: A live cell stays alive if it has 2–3 live neighbors (dies otherwise).  
- **Boundaries**:  
  - *Toroidal*: Grid wraps around (edge cells connect to the opposite edge).  
  - *Fixed*: Edge cells have no neighbors outside the grid.  

### 2. Key Features  
- **Initialization**: Start with random cells or predefined patterns (e.g., "glider" that moves across the grid, "block" that stays still).  
- **Grid Display**: Shows live/dead cells and stats (generation count, live cells).  
- **Updates**: Automatically advances to new generations, applying rules to every cell.  
- **User Control**:  
  - Pause/resume, speed up/slow down.  
  - Edit cells (toggle single cells or regions).  
  - Save/load simulations or undo changes.  

### 3. Simple Logic  
1. **Count Neighbors**: For each cell, count live neighbors (8 surrounding cells).  
2. **Apply Rules**:  
   - Dead cells with 3 live neighbors → alive.  
   - Live cells with <2 or >3 neighbors → dead.  
3. **Repeat**: Update the grid and show the new state.  

### 4. How to Use  
- Run the script, choose grid size/rules, and pick an initial pattern.  
- Use commands like:  
  - `space` to pause/resume.  
  - `+/-` to adjust speed.  
  - `z` to undo changes.  
  - `Ctrl+C` to exit.
 
# Conway's Game of Life: Code Structure & Dependencies  

## 1. Dependencies (Imported Tools)  
The code uses a few key Python libraries to work:  
- **`numpy`**: Handles the grid (2D array) for fast cell calculations (e.g., counting neighbors, updating states).  
- **`os`**: Clears the screen (works on Windows/macOS/Linux) to refresh the grid display.  
- **`time`**: Controls simulation speed (adds delays between generations).  
- **`json`**: Saves/loads game states (so you can pause and resume later).  
- **`sys`/`select`**: Lets users type commands without stopping the simulation.  

## 2. Code Structure  
The code is organized around a **`GameOfLife` class** (all core logic lives here) plus helper functions:  

### a. The `GameOfLife` Class  
This is the main "container" for the game. It has:  
- **Initialization (`__init__`)**: Sets up the grid, rules, and stats (e.g., how many cells are alive).  
- **Grid Setup (`initialize_grid`)**: Starts the grid with random cells or predefined patterns (like gliders).  
- **Display (`display_grid`)**: Shows the grid on screen with stats (generation, live cells).  
- **Rule Application (`update_grid`)**: Updates the grid for the next generation (kills/saves cells based on neighbor counts).  
- **User Controls**: Methods to edit cells (toggle single cells/regions), save/load states, undo actions, and pause the game.  

### b. Helper Functions  
- **`parse_rules`**: Turns rule strings (like "B3/S23") into usable instructions for the game.  
- **`main`**: The entry point—asks users for grid size/rules, then starts the simulation.  

### c. Simulation Loop  
The `run_interactive` method keeps the game going:  
- Updates the grid automatically (unless paused).  
- Listens for user commands (e.g., "space" to pause, "+" to speed up).  

In short: The class manages the game state and rules, while helper functions handle setup/input. Dependencies make grid math fast and user interaction smooth.

Start
  │
  ▼
Print welcome message
  │
  ▼
Prompt user for grid width & height (with validation: 5–100 / 5–50)
  │
  ▼
Create GameOfLife instance with given dimensions
  │
  ▼
Prompt user for rule string (e.g., "B3/S23")
  │
  ▼
Parse rule → extract birth & survival neighbor counts
  │
  ▼
Update game rules accordingly
  │
  ▼
Prompt user to choose initial pattern:
   - 'r': random
   - 'g': glider
   - 'b': block
   - 'l': blinker
   - 'h': beehive
  │
  ▼
Initialize grid based on selected pattern
  │
  ▼
Display initial grid and control instructions
  │
  ▼
Enter interactive main loop (run_interactive)
  │
  ├───────────────────────────────────────┐
  ▼                                       │
Display current grid + stats + commands   │
  │                                       │
  ▼                                       │
Wait for user input OR auto-update grid   │
  │                                       │
  ├─ If input received:                   │
  │     Parse command:                    │
  │       • 'u' → update rules            │
  │       • 't' → toggle single cell      │
  │       • 'a' → toggle region           │
  │       • 'c' → clear grid              │
  │       • 'r' → re-randomize            │
  │       • 'p' → pick preset pattern     │
  │       • 's' → set boundary type       │
  │       • '+'/'-' → adjust speed        │
  │       • ' ' → pause/resume            │
  │       • 'z' → undo                    │
  │       • 'q' → reset game              │
  │       • 'v' → save state              │
  │       • 'l' → load state              │
  │       • Enter → step once             │
  │                                       │
  ├─ Else (no input):                     │
  │     Automatically call update_grid()  │
  │                                       │
  ▼                                       │
Sleep for current interval (e.g., 0.5s)   │
  │                                       │
  └───────────────────────────────────────┘
  │
  ▼
(Loop continues until Ctrl+C or exit)
  │
  ▼
Catch KeyboardInterrupt
  │
  ▼
Print final statistics:
   - Total generations
   - Max/min/final living cells
  │
  ▼
End program
