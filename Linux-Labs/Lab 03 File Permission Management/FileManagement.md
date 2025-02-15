# **Linux File Permission Management **

This lab guide will walk you through the essential Linux commands for managing file permissions, ownership, and creation. By completing this lab, you'll gain hands-on experience with `touch`, `chown`, `chmod`, and `ls` commands.

---

## **Lab Objectives**
By the end of this lab, you will be able to:
1. Create files using the `touch` command.
2. Change file ownership using the `chown` command.
3. Modify file permissions using the `chmod` command.
4. View file details using the `ls` command.

---

## **Prerequisites**
- A Linux environment (physical machine, virtual machine, or cloud-based terminal).
- Basic familiarity with the Linux terminal.
- Sudo privileges (for changing ownership).

---

## **Lab Setup**
1. Open your terminal.
2. Ensure you are in your home directory:
   ```bash
   cd ~
   ```
3. Create a directory named `project` if it doesn't already exist:
   ```bash
   mkdir -p ~/project
   ```

---

## **Step 1: Create a File**
### **Task**
Create a new file named `target_file` in the `~/project` directory.

### **Steps**
1. Use the `touch` command to create the file:
   ```bash
   touch ~/project/target_file
   ```
2. Verify that the file was created:
   ```bash
   ls ~/project
   ```
   **Expected Output**:
   ```
   target_file
   ```

---

## **Step 2: Change File Ownership**
### **Task**
Change the owner of `target_file` to `user1` and the group to `group1`.

### **Steps**
1. Ensure the user `user1` and group `group1` exist. If not, create them:
   ```bash
   sudo adduser user1
   sudo groupadd group1
   ```
2. Change the ownership of `target_file` to `user1` and `group1`:
   ```bash
   sudo chown user1:group1 ~/project/target_file
   ```
3. Verify the ownership change:
   ```bash
   ls -l ~/project/target_file
   ```
   **Expected Output**:
   ```
   -rw-r--r-- 1 user1 group1 0 <date> target_file
   ```

---

## **Step 3: Set File Permissions**
### **Task**
Set the permissions of `target_file` to `rwxrw----`.

### **Steps**
1. Use the `chmod` command to set the permissions:
   ```bash
   chmod 760 ~/project/target_file
   ```
   - Explanation of `760`:
     - `7` (owner): Read (`4`) + Write (`2`) + Execute (`1`) = `7`
     - `6` (group): Read (`4`) + Write (`2`) = `6`
     - `0` (others): No permissions = `0`

2. Verify the permission change:
   ```bash
   ls -l ~/project/target_file
   ```
   **Expected Output**:
   ```
   -rwxrw---- 1 user1 group1 0 <date> target_file
   ```

---

## **Step 4: Practice Additional Commands**
To further solidify your understanding, try the following tasks:

### **Task 1: Add Execute Permission for Others**
1. Add execute permission for "others" on `target_file`:
   ```bash
   chmod o+x ~/project/target_file
   ```
2. Verify the change:
   ```bash
   ls -l ~/project/target_file
   ```
   **Expected Output**:
   ```
   -rwxrw---x 1 user1 group1 0 <date> target_file
   ```

### **Task 2: Remove Write Permission for Group**
1. Remove write permission for the group:
   ```bash
   chmod g-w ~/project/target_file
   ```
2. Verify the change:
   ```bash
   ls -l ~/project/target_file
   ```
   **Expected Output**:
   ```
   -rwxr-x--x 1 user1 group1 0 <date> target_file
   ```

### **Task 3: Reset All Permissions**
1. Reset all permissions to `rw-r--r--`:
   ```bash
   chmod 644 ~/project/target_file
   ```
2. Verify the change:
   ```bash
   ls -l ~/project/target_file
   ```
   **Expected Output**:
   ```
   -rw-r--r-- 1 user1 group1 0 <date> target_file
   ```

---

## **Step 5: Clean Up**
After completing the lab, clean up the files and directories you created:
1. Delete the `project` directory:
   ```bash
   rm -rf ~/project
   ```
2. Remove the `user1` user and `group1` group:
   ```bash
   sudo deluser user1
   sudo groupdel group1
   ```

---

## **Summary**
You have successfully completed the Linux File Permission Management Lab! Here's what you've learned:
1. **File Creation**: Used `touch` to create files.
2. **Ownership Management**: Changed file ownership with `chown`.
3. **Permission Management**: Modified file permissions with `chmod`.
4. **File Inspection**: Viewed file details with `ls`.

These skills are fundamental for Linux system administration and will help you manage files securely and effectively.

---

## **Additional Resources**
- [Linux `chmod` Command](https://man7.org/linux/man-pages/man1/chmod.1.html)
- [Linux `chown` Command](https://man7.org/linux/man-pages/man1/chown.1.html)
- [Linux `ls` Command](https://man7.org/linux/man-pages/man1/ls.1.html)

Happy learning and practicing! 🚀