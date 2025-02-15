# **Linux Lab: The Manuscript Mystery**

Welcome to the challenge "The Manuscript Mystery." In this lab, you'll use Linux commands to examine and compare two versions of a manuscript page. By completing this lab, you'll demonstrate your ability to work with file contents and compare files using essential Linux tools.

# **Introduction**

As a junior editor at a publishing house, you've stumbled upon two versions of a crucial page from an upcoming mystery novel. Your task is to examine these files using the Linux commands you've just learned in the File Contents and Comparing lab.

## **Achievements**

Upon completing this challenge, you will demonstrate your ability to:

- Use `cat` to view file contents
- Use `head` and `tail` to examine specific parts of files
- Compare files using the `diff` command

# **Examining File Contents**

In this step, you'll use `cat`, `head`, and `tail` to inspect two mysterious files.

## **Tasks**

1. Use `cat` to view the contents of `/home/poridhi/project/manuscript_v1.txt`.
2. Use `head` -n2 to view the **first two lines** of `/home/poridhi/project/manuscript_v2.txt`.
3. Use `tail` -n1 to view **the last line** of both files.

## **Requirements**

- Use only the commands learned in the File Contents and Comparing lab (`cat`, `head`, `tail`).
- Do not modify the contents of the files.

---

---

## **Lab Setup**

Before starting, ensure you have access to a Linux terminal with the following files:

- `/home/labex/project/manuscript_v1.txt`
- `/home/labex/project/manuscript_v2.txt`

These files contain two versions of the same manuscript page.

---

## **Step 1: Examining File Contents**

### **Task 1: View the Full Contents of `manuscript_v1.txt`**

Use the `cat` command to view the entire contents of `manuscript_v1.txt`.

**Command:**

```bash
cat /home/labex/project/manuscript_v1.txt

```

**Expected Output:**

```
The room was dimly lit, shadows dancing on the walls.
A shadow moved across the room.
The clock struck midnight, echoing through the silence.

```

---

### **Task 2: View the First Two Lines of `manuscript_v2.txt`**

Use the `head` command with the `-n2` option to display the first two lines of `manuscript_v2.txt`.

**Command:**

```bash
head -n2 /home/labex/project/manuscript_v2.txt

```

**Expected Output:**

```
The room was dimly lit, shadows dancing on the walls.
A figure darted behind the curtains.

```

---

### **Task 3: View the Last Line of Both Files**

Use the `tail` command with the `-n1` option to display the last line of both files.

**Commands:**

```bash
tail -n1 /home/labex/project/manuscript_v1.txt
tail -n1 /home/labex/project/manuscript_v2.txt

```

**Expected Outputs:**
For `manuscript_v1.txt`:

```
The clock struck midnight, echoing through the silence.

```

For `manuscript_v2.txt`:

```
The clock struck midnight, but no one was there to hear it.

```

---

## **Step 2: Comparing the Files**

### **Task 4: Compare the Two Files**

Use the `diff` command to identify differences between `manuscript_v1.txt` and `manuscript_v2.txt`.

**Command:**

```bash
diff /home/labex/project/manuscript_v1.txt /home/labex/project/manuscript_v2.txt

```

**Expected Output:**

```
2c2
< A shadow moved across the room.
---
> A figure darted behind the curtains.
3c3
< The clock struck midnight, echoing through the silence.
---
> The clock struck midnight, but no one was there to hear it.

```

---

## **Step 3: Analyze the Differences**

### **Explanation of the `diff` Output**

The `diff` output shows that:

1. **Line 2** differs:
    - In `manuscript_v1.txt`: `A shadow moved across the room.`
    - In `manuscript_v2.txt`: `A figure darted behind the curtains.`
2. **Line 3** differs:
    - In `manuscript_v1.txt`: `The clock struck midnight, echoing through the silence.`
    - In `manuscript_v2.txt`: `The clock struck midnight, but no one was there to hear it.`

This indicates that the second version (`manuscript_v2.txt`) provides more specific imagery and alters the tone slightly compared to the first version.

---

---

## **Summary**

Congratulations, junior editor! You've successfully completed "The Manuscript Mystery" lab. By using `cat`, `head`, `tail`, and `diff`, you've demonstrated your ability to:

- View file contents.
- Examine specific parts of files.
- Compare files to identify differences.

These skills are essential for working with text files in Linux and will serve you well in both editorial and technical roles.