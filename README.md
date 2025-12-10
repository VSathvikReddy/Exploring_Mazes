<style>
/* ---- Dark Theme Markdown Style (Forced) ---- */

body {
  background: #0d1117 !important;
  color: #c9d1d9 !important;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif !important;
  line-height: 1.65 !important;
  padding: 2rem !important;
}
/* Headings */
h1 strong {
  color: #b52828ff !important;   /* change this to whatever color you want */
  font-weight: 7000 !important;
}

h2, h3, h4, h5, h6 {
  color: #e6edf3 !important;
  margin-top: 1.6em !important;
  margin-bottom: 0.6em !important;
  font-weight: 600 !important;
}
h1{
  color: #2874b5ff !important;
  margin-top: 0.5em !important;
  margin-bottom: 0.6em !important;
  font-weight: 600 !important;
}
h1 {
  padding-bottom: .3em !important;
}
h2{
  color: #b52828ff !important;
  margin-top: 1.6em !important;
  margin-bottom: 0.6em !important;
  font-weight: 600 !important;
}

/* Paragraphs & Text */
p {
  margin: 0.9em 0 !important;
}
strong {
  color: #b43a3aff !important;
}
em {
  color: #73787eff !important;
}

/* Links */
a {
  color: #ff5858ff !important;
  text-decoration: none !important;
}
a:hover {
  text-decoration: underline !important;
}

/* Inline code */
code {
  background: #161b22 !important;
  color: #e6edf3 !important;
  padding: 2px 4px !important;
  border-radius: 4px !important;
  font-size: 0.95em !important;
}

/* Code blocks */
pre {
  background: #161b22 !important;
  padding: 1rem !important;
  border-radius: 6px !important;
  overflow-x: auto !important;
  border: 1px solid #30363d !important;
}

pre code {
  background: none !important;
  padding: 0 !important;
}

/* Blockquotes */
blockquote {
  border-left: 4px solid #30363d !important;
  padding-left: 1rem !important;
  color: #8b949e !important;
  margin: 1.2em 0 !important;
}

/* Lists */
ul, ol {
  margin: 0.8em 0 0.8em 1.2em !important;
}

li {
  margin: 0.4em 0 !important;
}

/* Tables */
table {
  border-collapse: collapse !important;
  width: 100% !important;
  margin: 1em 0 !important;
}

th, td {
  border: 1px solid #30363d !important;
  padding: 0.6em !important;
}

th {
  background: #161b22 !important;
  color: #e6edf3 !important;
}

/* Horizontal Rule */
hr {
  border: 0 !important;
  border-top: 1px solid #30363d !important;
  margin: 2em 0 !important;
}
.box {
  border: 1px solid #30363d;
  background: #161b22;
  padding: 1rem;
  border-radius: 6px;
  margin-top: 0 !important;   /* remove space on top */
  margin-bottom: 1rem !important; /* optional bottom spacing */
  color: #c9d1d9;
}
</style>


# <center>MAZE TIME!!!!</center>

---

## 1. Executing the files


1. The following comand should help you setup SFML Library which was used for rendering. I had Version: 2.5.1 _(latest allowed for ubuntu)_, but hopefully should work on any newer version.
   ```bash
   make setup
   ```
2. To compile all the files and create the executable 

   ```bash
    make
   ```
   or
    ```bash
    make compile
    ```
3. To run the game
    ```bash
    ./a.out
    ```
    or you wanna look cool 😎
    ```bash
    make run
    ```
4. This command was used by me to merge my png images together, to create the final textures.png, there is no immediate need to understand this.
    ```bash
    make images
    ```

---

## 2. Controling the window
After executing the program, you'll see the player, blue blob move around. You can,

- *Space Bar* to pause  
- *Right Arrow* to speed up
- *Left Arrow* to slowdown.
- Click the Close *(X)* Button on the window → closes the window and exits the game, and displays your score.

If the game is completed, the game is automatially paused.

---

# What even is the game.

Run the game for a while, and you can see the blob is in it's starting position and not moving.
- The blob guys is supposed to explore the maze, encoded in `Player.think()`
- There are 4 type of tiles, as in the blobs memory

| Color Name | Color | Number in memory | Meaning |
|-----------|--------|------------------|---------|
| Black     | <span style="display:inline-block; width:18px; height:18px; background:#000000; border:1px solid #555; margin-top:4px;"></span> | `0` | Uexplored tile |
| Dark Gray | <span style="display:inline-block; width:18px; height:18px; background:#555555; border:1px solid #555; margin-top:4px;"></span> | `1` | Visited Path |
| Light Gray| <span style="display:inline-block; width:18px; height:18px; background:#DDDDDD; border:1px solid #555; margin-top:4px;"></span> | `2` | Wall |
| Yellow    | <span style="display:inline-block; width:18px; height:18px; background:#FFD700; border:1px solid #555; margin-top:4px;"></span> | `3` | Goal |

- The blob has a 3X3 vision* around it. It moves according to the function `Player.think()`, at the start.
- Once it steps onto the *Goal Tile* it finds the shortest route (according to it's memory) to the starting point and goes, as per `Player.gotoTarget(0,0)`. (This is how shortest path is calculated of your run)

---

## 3. What should you do
 
`script.cpp` is the only file I would like you to modify. It has a child class of player, for you to implement and play with,

- ~~(Due to impatience)~~, both `Player.gotoTarget()` and `Player.Think()` are very horriblly implemented
- So they have been declared as `virtual` functions _(you'll learn more about the later)_, for you to override in the child class.
- Learn some nice maze solving algorithms, and implement them in the Think() member function.
- You may have multiple paths to the goal

|$Score = \sqrt{TimeSpent}*ShortestDistanceFound$ |
|----------------------------------|

- Even after you discover the goal, the `gotoTarget(0,0)`, activates once you step on it, so you can still explore for other routes.
