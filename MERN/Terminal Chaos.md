


- **WinGet** installs native Windows machinery (compiled `.exe` apps like `fzf`, `bat`, Chrome, VS Code).
    
- **NPM** installs web machinery (JavaScript tools like `tldr`, `live-server`, React, or Vite).



----

### Git Bash cmd -
#### 1. Navigating Your Files & Folders

Think of these as your way of looking around and moving through your project folders.

- **`pwd`** (Print Working Directory): Shows the exact folder path you are currently standing in.
    
- **`ls`** (List): Lists all files and folders in your current directory.
    
    - `ls -a`: Shows hidden files (like `.env` or `.gitignore`).
        
    - `ls -l`: Shows a detailed list with file sizes and permissions.
        
- **`cd <folder>`** (Change Directory): Moves you inside a specific folder (e.g., `cd server`).
    
- **`cd ..`**: Moves you backward/up one folder level.
    
- **`cd ~`**: Takes you straight back to your computer's main user home directory.
    

---

#### 2. Managing Files & Folders

Instead of right-clicking to create or delete things, use these to do it instantly.

- **`touch <filename>`**: Creates a brand new, empty file (e.g., `touch index.js`).
    
- **`mkdir <foldername>`** (Make Directory): Creates a new folder (e.g., `mkdir routes`).
    
- **`cp <source> <destination>`** (Copy): Copies a file from one place to another.
    
- **`mv <source> <destination>`** (Move/Rename): Moves a file to a new folder, or renames it if kept in the same folder.
    
- **`rm <filename>`** (Remove): Permanently deletes a file. _(Be careful, this bypasses the Recycle Bin!)_
    
- **`rm -rf <foldername>`**: Force-deletes an entire folder and everything inside it.
    

---

#### 3. Viewing & Editing Files Quickly

Sometimes you just want to check what's inside a file without opening VS Code.

- **`cat <filename>`**: Dumps the entire contents of a file right into your terminal window.
    
- **`head -n 10 <filename>`**: Shows just the first 10 lines of a file.
    
- **`tail -n 10 <filename>`**: Shows the last 10 lines of a file (great for checking server logs).
    
- **`nano <filename>`**: Opens a very basic text editor right inside the terminal for quick edits.
    

---

#### 4. System & Process Commands

These help you monitor your environment and stop running code.

- **`clear`**: Cleans up a messy terminal screen (Shortcut: `Ctrl + L`).
    
- **`printenv`**: Lists all active environment variables on your system.
    
- **`history`**: Lists the last few hundred commands you've typed in case you forgot one.
    
- **`Ctrl + C`**: _The universal panic button._ It kills whatever server or script is currently running in your terminal so you can type a new command.
    

---

## 💡 Pro-Tips for Git Bash

- **Tab Completion:** Type the first two letters of a folder name and hit `Tab`. Git Bash will auto-fill the rest for you.
    
- **Arrow Keys:** Press the **Up Arrow ($\uparrow$)** to cycle through commands you previously typed so you don't have to re-enter them.
