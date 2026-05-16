## **Task 1: Editing Files with `vim` and `nano`**

### **Subtask 1.1: Create/Edit Files with `vim`**
1. Open a file named `lab5_vim.txt`:
   ```bash
   vim lab5_vim.txt
Press i to enter Insert Mode and add the following text:
Red Hat Enterprise Linux
Text Editing Lab
Version 9.0
Save and exit:
Press ESC → Type :wq → Press Enter
Expected Outcome:
File lab5_vim.txt is created with the specified content.

Troubleshooting:

If you exit without saving (:q!), changes are discarded.
Use :w to save without exiting.
Subtask 1.2: Edit Files with nano
Open/create lab5_nano.txt:
nano lab5_nano.txt
Add the following text:
Nano is a user-friendly editor.
Used for quick edits.
Save and exit:
Press Ctrl+O → Enter → Ctrl+X
Key Concept:
nano shows keybindings at the bottom, making it beginner-friendly.

Task 2: Inline Text Replacement with sed
Subtask 2.1: Replace Text in a File
Create a sample file:
echo -e "RHEL 8\nRHEL 9\nFedora 38" > versions.txt
Replace "RHEL" with "Red Hat":
sed -i 's/RHEL/Red Hat/g' versions.txt
Verify:
cat versions.txt
Expected Output:
Red Hat 8
Red Hat 9
Fedora 38
Troubleshooting:

Use sed -i.bak to create a backup before editing.
Subtask 2.2: Delete Lines Matching a Pattern
Delete lines containing "Fedora":
sed -i '/Fedora/d' versions.txt
Verify:
cat versions.txt
Expected Output:
Red Hat 8
Red Hat 9
Task 3: Text Processing with awk
Subtask 3.1: Extract Specific Columns
Create a CSV file:
echo -e "ID,Name,OS\n1,Alice,RHEL\n2,Bob,Fedora" > users.csv
Extract the "Name" column (2nd field):
awk -F ',' '{print $2}' users.csv
Expected Output:
Name
Alice
Bob
Subtask 3.2: Filter Rows Based on Condition
Print rows where OS is "RHEL":
awk -F ',' '$3 == "RHEL" {print $0}' users.csv
Expected Output:
1,Alice,RHEL
Key Concept:
awk uses -F to specify field separators (e.g., , for CSV).
