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
