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

flowchart TD
    A[Start] --> B[Print welcome message]
    B --> C[Prompt for grid width & height\n(Validate: 5–100 × 5–50)]
    C --> D[Create GameOfLife instance]
    D --> E[Prompt for rule string\n(e.g., 'B3/S23')]
    E --> F[Parse rules → birth & survival lists]
    F --> G[Update game rules]
    G --> H[Choose initial pattern:\n r=random, g=glider, b=block,\n l=blinker, h=beehive]
    H --> I[Initialize grid with pattern]
    I --> J[Display grid + control instructions]
    J --> K{Enter interactive loop}
    
    K --> L[Render current grid,\nstats, and command menu]
    L --> M{User input?}
    
    M -- Yes --> N[Parse command]
    N --> O1['u': update rules]
    N --> O2['t': toggle single cell]
    N --> O3['a': toggle region]
    N --> O4['c': clear grid]
    N --> O5['r': re-randomize]
    N --> O6['p': select preset pattern]
    N --> O7['s': set boundary type]
    N --> O8['+/-': adjust speed]
    N --> O9['space': pause/resume]
    N --> O10['z': undo]
    N --> O11['q': reset game]
    N --> O12['v': save state]
    N --> O13['l': load state]
    N --> O14['Enter': step once]
    
    M -- No --> P[Auto-update grid via update_grid()]
    
    O1 --> Q
    O2 --> Q
    O3 --> Q
    O4 --> Q
    O5 --> Q
    O6 --> Q
    O7 --> Q
    O8 --> Q
    O9 --> Q
    O10 --> Q
    O11 --> Q
    O12 --> Q
    O13 --> Q
    O14 --> Q
    P --> Q
    
    Q --> R[Sleep for current interval\n(e.g., 0.5s)]
    R --> K
    
    K --> S{Ctrl+C or exit?}
    S -- Yes --> T[Print final stats:\n- Total generations\n- Max/min/final living cells]
    T --> U[End program]
