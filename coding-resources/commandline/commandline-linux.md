---
layout: page
title: Linux
parent: Command Line
grand_parent: Coding Resources
nav_order: 2
---

# Simple Intro to the Linux Command Line (bash)

This is a minimal, practical cheat sheet for everyday tasks on Linux (bash).  
Most of this works the same in other shells too.

---

## 0) Open a terminal

- Usually: Applications → Terminal  
- Common shortcut: **Ctrl + Alt + T** (varies by distro)

---

## 1) Core ideas

### Your location (current folder)
- Show current folder:
```bash
pwd
```
- List files:
```bash
ls
```

### Paths
- `.` means “this folder”
- `..` means “parent folder”
- `/` is the path separator

Examples:
```bash
cd .
cd ..
cd /home/yourname/Downloads
```

### Autocomplete + history
- Press **Tab** to autocomplete.
- Use **↑ / ↓** for command history.

---

## 2) Navigate folders

- Change folder:
```bash
cd <path>
```

Examples:
```bash
cd Documents
cd ..
cd ~
```

- `~` is your home folder.

---

## 3) Create, copy, move, delete

### Create a folder
```bash
mkdir <foldername>
```

### Create an empty file
```bash
touch <filename>
```

### Copy
```bash
cp <source> <destination>
```

### Move / rename
```bash
mv <source> <destination>
```

If you do not know the <source> and <destination>, you can use the autocomplete feature to find them.
You can also drag and drop the files from the File Explorer into the terminal window to find the paths.

### Delete (be careful)
- Delete a file:
```bash
rm <filename>
```
- Delete a folder and everything inside:
```bash
rm -r <foldername>
```

> Tip: If you are unsure, run `ls` first and double-check the path.

---

## 4) View file contents

- Print a text file:
```bash
cat <filename>
```

- View long output one screen at a time:
```bash
less <filename>
```
(Press `q` to quit.)

---

## 5) Search (basic)

- Find files/folders by name:
```bash
find . -name "*partialname*"
```

- Search inside files for text:
```bash
grep -R "text" .
```
---

## Quick safety rules

- If you do not know what a command does, do not run it :)
- Be extra careful with `rm` (especially `rm -r`).
- Quote paths with spaces:
```bash
cd "My Folder"
```

---

## A tiny practice routine (2 minutes)

```bash
mkdir cli-practice
cd cli-practice
touch notes.txt
ls
echo "hello" >> notes.txt
cat notes.txt
cd ..
rm -r cli-practice
```
