---
layout: page
title: Windows
parent: Command Line
grand_parent: Coding Resources
nav_order: 3
---

# Simple Intro to the Windows Command Line (PowerShell)

This is a minimal, practical cheat sheet for everyday tasks. It assumes PowerShell (the default on modern Windows).  
(If you are in Command Prompt (cmd.exe), some commands differ see notes below.)

---

## 0) Open a terminal

- **Windows Terminal** (recommended): Start menu → “Windows Terminal”
- **PowerShell**: Start menu → “PowerShell”

---

## 1) Core ideas

### Your location (current folder)
- Show current folder:
```powershell
pwd
```
- List files:
```powershell
ls
```

### Paths
- `.` means “this folder”
- `..` means “parent folder”
- `\` is the Windows path separator (PowerShell also accepts `/` in many cases)

Examples:
```powershell
cd .
cd ..
cd C:\Users\YourName\Downloads
```

### Autocomplete
- Press **Tab** to autocomplete paths/commands.
- Use **Up arrow** to cycle command history.

---

## 2) Navigate folders

- Change folder:
```powershell
cd <path>
```

Examples:
```powershell
cd Documents
cd .. 
cd C:\Windows
```

- Go back to your home folder:
```powershell
cd ~
```

---

## 3) Create, copy, move, delete

### Create a folder
```powershell
mkdir <foldername>
```

### Create an empty file
```powershell
New-Item <filename> -ItemType File
```

### Copy
```powershell
cp <source> <destination>
```

### Move / rename
```powershell
mv <source> <destination>
```

If you do not know the <source> and <destination>, you can use the autocomplete feature to find them.
You can also drag and drop the files from the File Explorer into the terminal window to find the paths.

### Delete (be careful)
- Delete a file:
```powershell
rm <filename>
```
- Delete a folder and everything inside:
```powershell
rm <foldername> -Recurse
```

> Tip: If you are unsure, run `ls` first and double-check the path.

---

## 4) View file contents

- Print a text file:
```powershell
cat <filename>
```

- View long output one screen at a time:
```powershell
cat <filename> | more
```

---

## 5) Search (basic)

- Find files/folders by name (current folder and below):
```powershell
Get-ChildItem -Recurse -Filter "*partialname*"
```

- Search inside files for text:
```powershell
Select-String -Path .\* -Pattern "text"
```


## Quick safety rules

- If you do not know what a command does, do not run it :)
- Be extra careful with delete commands (`rm`, especially with `-Recurse`).
- Quote paths with spaces:
```powershell
cd "C:\Users\Your Name\My Folder"
```

---

## A tiny practice routine (2 minutes)

```powershell
mkdir cli-practice
cd cli-practice
New-Item notes.txt -ItemType File
ls
echo "hello" >> notes.txt
cat notes.txt
cd ..
rm cli-practice -Recurse
```
