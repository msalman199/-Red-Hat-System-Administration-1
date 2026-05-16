# Editing Text Files in RHEL

This repository contains a hands-on lab focused on configuring, parsing, and transforming text data on a Red Hat Enterprise Linux system using interactive CLI text editors (`vim`, `nano`) and stream-processing utilities (`sed`, `awk`).

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- Create and modify text configuration files using both modal (`vim`) and modeless (`nano`) command-line text editors.
- Perform high-speed inline text search, replacement, and structural deletions using `sed`.
- Filter, isolate, and format structured matrix data (like CSV formats) using `awk` conditional patterns.

## 📋 Prerequisites
- A RHEL 8/9 operating system environment (CentOS Stream or Fedora are acceptable alternatives).
- Terminal access featuring elevated `sudo` system administration privileges.
- Basic familiarity running elementary core Linux command strings.

---

## 🛠️ Lab Tasks

### Task 1: Editing Files with vim and nano

#### Subtask 1.1: Create/Edit Files with vim
1. Launch the Vim text editor engine to create or modify a file named `lab5_vim.txt`:
   ```bash
   vim lab5_vim.txt
   ```
2. **Input Mode Transition**: Press the `i` key to transition Vim into **Insert Mode**, then manually append the following text configuration block:
   ```text
   Red Hat Enterprise Linux
   Text Editing Lab
   Version 9.0
   ```
3. **Commit & Close**: Hit the `Esc` key to return to Command Mode, type out the sequence `:wq`, and press `Enter` to write out files changes and quit.

💡 **Troubleshooting**: If you need to abort without committing modifications, execute the `:q!` escape sequence. To write out changes to the disk storage block *without* dropping out of your active editor instance, execute `:w`.

#### Subtask 1.2: Edit Files with nano
1. Spawn an editor workspace tracking `lab5_nano.txt` using the Nano buffer wrapper:
   ```bash
   nano lab5_nano.txt
   ```
2. Enter the following plain text into the editor window:
   ```text
   Nano is a user-friendly editor.
   Used for quick edits.
   ```
3. **Commit & Close**: Press `Ctrl+O` followed by `Enter` to write the storage block, then strike `Ctrl+X` to terminate the active interface.

📌 **Key Concept**: Unlike Vim, Nano features static keybinding action keys directly along the baseline of the active viewer screen. This design minimizes the initial learning curve for beginners.

---

### Task 2: Inline Text Replacement with sed

#### Subtask 2.1: Replace Text in a File
1. Use an echoing pipe wrapper to spin up a plain target file:
   ```bash
   echo -e "RHEL 8\nRHEL 9\nFedora 38" > versions.txt
   ```
2. Target global occurrences of the substring "RHEL" and execute an inline swap replacing them with the string "Red Hat":
   ```bash
   sed -i 's/RHEL/Red Hat/g' versions.txt
   ```
3. Check the internal file updates:
   ```bash
   cat versions.txt
   ```
   *Expected Output:*
   ```text
   Red Hat 8
   Red Hat 9
   Fedora 38
   ```

💡 **Troubleshooting**: You can run `sed -i.bak 's/search/replace/g' filename` to automatically force the system to backup your source code state into a separate `.bak` copy before performing regex swaps.

#### Subtask 2.2: Delete Lines Matching a Pattern
1. Strip out lines that match target terms (like "Fedora") entirely from your active data pool:
   ```bash
   sed -i '/Fedora/d' versions.txt
   ```
2. Re-read the file output layout structure:
   ```bash
   cat versions.txt
   ```
   *Expected Output:*
   ```text
   Red Hat 8
   Red Hat 9
   ```

---

### Task 3: Text Processing with awk

#### Subtask 3.1: Extract Specific Columns
1. Build out a mock comma-separated matrix file containing system entities:
   ```bash
   echo -e "ID,Name,OS\n1,Alice,RHEL\n2,Bob,Fedora" > users.csv
   ```
2. Target field dimensions to parse out and extract only the target column element (the second index position):
   ```bash
   awk -F ',' '{print $2}' users.csv
   ```
   *Expected Output:*
   ```text
   Name
   Alice
   Bob
   ```

#### Subtask 3.2: Filter Rows Based on Condition
1. Use structured string checking loops to dump rows matching criteria matching exactly against position 3:
   ```bash
   awk -F ',' '\$3 == "RHEL" {print \$0}' users.csv
   ```
   *Expected Output:* `1,Alice,RHEL`

📌 **Key Concept**: Awk references the explicit field boundaries delimiter matrix via the `-F` parameter flag (e.g., passing `,` changes operational loops to recognize standard CSV grids).

---

## 🏁 Conclusion
During this lab session, you developed foundational text manipulation skills, including:
- Accessing text files with native command-line editors (`vim` and `nano`).
- Engineering inline, rapid string swaps and pattern deletions with `sed`.
- Filtering structured arrays using field boundaries with `awk`.

## 🚀 Next Steps
- Chain these stream editors directly with piping commands (`|`) inside your shell deployment structures to parse system access log files.
- Dive into advanced regex parameter flags within core manuals to build highly automated pattern structures.

---

## 🔎 Final Verification Lookup
Confirm that all relevant files were generated and modified correctly in your terminal folder path:
```bash
ls -l lab5_*.txt versions.txt users.csv
```

---

## 📚 Additional Resources
- Local documentation lookups: `man vim`, `man nano`, `man sed`, `man awk`
- [GNU sed Manual Pages](https://gnu.org)
- [AWK Programming Guide](https://gnu.org)
