# 2048 Game

This is a web-based implementation of the classic puzzle game **2048**, built entirely with HTML, CSS, and vanilla JavaScript.

---

## 🚀 Overview

The goal of the game is to slide numbered tiles on a $4 \times 4$ grid to combine them and create a tile with the number **2048**. The game continues until a player achieves higher tiles (like 4096 and 8192) or runs out of valid moves.

---

## ⚙️ Technology Stack

* **HTML (index.html):** Provides the structure for the game board (`#board`), the score display (`#score`), and the overall page layout.
* **CSS (index.css):** Styles the game, setting the grid layout, board appearance, and providing distinct **colors** and **styles** for each numbered tile (from 'x2' up to 'x8192').
* **JavaScript (index.js):** Contains the entire game logic, including board initialization, tile movement, merging, scoring, and win/loss condition checking.

---

## 🧩 Core Game Logic (index.js Analysis)

The JavaScript file manages the entire state and functionality of the game.

### Board & Initialization
* **`board`**: A $4 \times 4$ array initialized to all zeros (`[[0,0,0,0],...]`) to represent the game grid.
* **`setGame()`**:
    * Initializes the `board` array.
    * Dynamically creates 16 `div` elements for the tiles, assigning them unique IDs (e.g., "0-0", "3-3").
    * Appends these tile elements to the HTML `#board`.
    * Calls `setTwo()` twice to place the starting '2' tiles.

### Movement and Sliding
The core sliding and merging logic is separated into a few key functions:
1.  **`handleSlide(e)`**: The event listener attached to `document.addEventListener("keydown")`. It detects arrow key presses, prevents default scrolling, and calls the appropriate directional slide function (`slideLeft`, `slideRight`, etc.).
2.  **`filterZero(row)`**: Takes an array (a row or a column) and returns a new array with all the `0`s removed.
3.  **`slide(row)`**:
    * Performs the actual merge logic. It takes a filtered row/column, iterates through it, and **doubles** tiles that are equal and adjacent, setting the second tile to `0`.
    * Updates the global **`score`**.
    * Filters the zeros again.
    * Pads the array with zeros (`0`) until its length is 4.
    * Returns the final, slid, and merged array.
4.  **Directional Slides (`slideLeft`, `slideRight`, `slideUp`, `slideDown`)**:
    * **Horizontal slides** (`slideLeft`, `slideRight`) work directly on rows (`board[r]`).
    * **Vertical slides** (`slideUp`, `slideDown`) first extract a **column** into a temporary array, call `slide()` on it, and then place the values back into the `board` array.
    * The **reverse** method is used for `slideRight` and `slideDown` to allow the `slide()` function to always process merges towards the start of the temporary array.

### Tile Generation and Updates
* **`setTwo()`**: Responsible for randomly placing a new '2' tile on any empty spot (`0`) on the board after a successful move. It uses `Math.random()` to find a random empty coordinate.
* **`updateTile(tile, num)`**: Synchronizes the visual representation of a tile with the numerical value in the `board` array. It clears existing classes and adds the appropriate **CSS class** (e.g., `x2`, `x2048`) based on the tile's value.

### Game State Checks
* **`canMoveLeft/Right/Up/Down()`**: These functions check if a move is possible in a given direction, preventing unnecessary sliding and tile generation if no tiles would move or merge.
* **`hasLost()`**: Returns `true` if there are no empty tiles *and* no adjacent tiles have the same value, indicating the board is full and no further moves can be made.
* **`checkWin()`**: Alerts the player when they reach 2048, 4096, and 8192 for the first time, using boolean flags (`is2048Exist`, etc.) to prevent repeat alerts.
* **`restartGame()`**: Simply reloads the page to start a new game.

---

## ✨ Styling (index.css Analysis)

The CSS defines a clean, functional style typical of the 2048 game:

* **`#board`**: A fixed $400\text{px} \times 400\text{px}$ container using `display: flex` and `flex-wrap: wrap` to arrange the tiles in a grid.
* **`.tile`**: Sets the basic dimensions, borders, and centers the text content using `display: flex` with `justify-content: center` and `align-items: center`.
* **Tile Specific Classes (`.x2`, `.x4`, ... `x8192`)**: Each class provides a unique `background-color` and `color` to visually distinguish the value of the tile, providing immediate feedback to the player.

---

## 🛠️ How to Run

1.  Save all four files (`index.html`, `index.css`, `index.js`, and `README.md`) into the same folder.
2.  Open **`index.html`** in any modern web browser.
3.  Use the **Arrow Keys** (Left, Right, Up, Down) to play the game!

---

## 👤 Credits

* **Creator:** KaijuBytes
* **Concept:** The 2048 game, originally created by Gabriele Cirulli.
