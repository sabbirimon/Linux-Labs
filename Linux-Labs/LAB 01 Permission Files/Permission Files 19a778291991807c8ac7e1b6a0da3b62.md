# Permission Files

# **Introduction**

In this lab, we'll dive into the world of file permissions in Linux. We'll explore three essential commands: `chown`, `touch`, and `chmod`. These tools are crucial for managing access to files and directories on a Linux system. By the end of this lab, you'll have a solid grasp on creating files, changing file ownership, and modifying file permissions. Understanding these commands will empower you to control who can read, write, and execute files on your system.

## **Achievements**

After completing this lab, you'll be able to:

- Use `chmod` to modify file permissions
- Use `chown` to change file ownership
- Use `touch` to create new files and update timestamps of existing files

# **Creating a New File**

Let's start by creating a new file using the `touch` command. This versatile command can create new, empty files and update the timestamps of existing ones. Think of it as a quick way to "touch" a file, either bringing it into existence or updating its last accessed time.

First, make sure you're in the right directory. We'll be working in your `project` directory:

```bash
cd ~/project 
```

The `cd` command stands for "change directory." The `~` symbol represents your home directory, and `/project` specifies the subdirectory we want to move into. If the `project` directory doesn't exist, this command will likely fail. It's generally a good practice to create the directory first if you're unsure. However, in this lab environment, the directory should already exist.

Now, let's create a new file named `example.txt`:

```bash
touch example.txt 
```

This command creates an empty file called `example.txt` in your current directory. To confirm that the file was created, use the `ls` command:

```bash
ls 
```

`ls` stands for "list." It shows you the files and directories in your current location. You should see `example.txt` listed in the output. If you don't see it, double-check that you ran the `touch` command correctly and that you are indeed in the `~/project` directory.

![Screenshot 2568-02-14 at 8.08.56 AM.png](Permission%20Files%2019a778291991807c8ac7e1b6a0da3b62/Screenshot_2568-02-14_at_8.08.56_AM.png)

# **Changing the Ownership of a File**

Now that we've created a file, let's learn how to change its ownership. The `chown` command allows us to modify both the user and group ownership of a file. Ownership determines who has control over the file.

First, let's check the current ownership of our `example.txt` file:

```bash
ls -l example.txt 
```

The `ls -l` command (list with long format) provides detailed information about the file, including its permissions, owner, and group. You should see output similar to this:

![Screenshot 2568-02-14 at 8.12.19 AM.png](Permission%20Files%2019a778291991807c8ac7e1b6a0da3b62/Screenshot_2568-02-14_at_8.12.19_AM.png)

```
-rw-rw-r-- 1 labex labex 0 Jul 29 15:11 example.txt 
```

Let's break down this output:

1. `rw-rw-r--` represents the file permissions (we'll explore this more in Step 4). The first character indicates the file type ( `` for a regular file, `d` for directory, etc.). The remaining characters represent read, write, and execute permissions for the owner, group, and others.
2. The first `labex` is the current owner of the file. This is the username that owns the file.
3. The second `labex` is the current group of the file. A group is a collection of users that can share permissions.
4. `0` is the file size in bytes. Since the file is empty, its size is zero.
5. `Jul 29 15:11` is the last modified date and time.
6. `example.txt` is the file name.

Now, let's change the ownership of the file to the `root` user. `root` is the administrator account on Linux systems, and it has special privileges.

```bash
sudo chown root:root example.txt 
```

Here's what this command does:

- `sudo` runs the command with root privileges. You'll likely be prompted for your password. `chown` requires elevated privileges because it's a powerful command that can affect system security. Without `sudo`, you'll get a "Permission denied" error.
- `chown` is the command to change ownership.
- `root:root` specifies the new owner and group (both set to root). The syntax is `owner:group`.
- `example.txt` is the target file.

Let's verify the change:

```bash
ls -l example.txt 
```

You should now see that both the owner and group have changed to `root`:

![Screenshot 2568-02-14 at 8.17.30 AM.png](Permission%20Files%2019a778291991807c8ac7e1b6a0da3b62/Screenshot_2568-02-14_at_8.17.30_AM.png)

```
-rw-rw-r-- 1 root root 0 Jul 29 15:11 example.txt 
```

If you still see `labex` instead of `root`, make sure you used `sudo` when running the `chown` command and entered your password correctly.

# **Changing the Ownership of a Directory**

The `chown` command can also change the ownership of entire directories and their contents. Let's see this in action. This is particularly useful for managing complex directory structures where you want to ensure all files and subdirectories have the same owner.

First, let's create a new directory with some files:

```bash
mkdir -p new-dir/subdir
echo "Hello, world" > new-dir/file1.txt
echo "Another file" > new-dir/subdir/file2.txt 
```

![Screenshot 2568-02-14 at 8.20.22 AM.png](Permission%20Files%2019a778291991807c8ac7e1b6a0da3b62/Screenshot_2568-02-14_at_8.20.22_AM.png)

Let's break down these commands:

- `mkdir -p new-dir/subdir` creates the `new-dir` directory and its `subdir` subdirectory. The `p` option tells `mkdir` to create parent directories as needed. Without `p`, if `new-dir` didn't exist, creating `new-dir/subdir` would fail.
- `echo "Hello, world" > new-dir/file1.txt` creates a file named `file1.txt` inside the `new-dir` directory and writes the text "Hello, world" into it. The `>` symbol is used for redirection; it takes the output of the `echo` command and redirects it into the specified file.
- `echo "Another file" > new-dir/subdir/file2.txt` similarly creates a file named `file2.txt` inside the `new-dir/subdir` directory and writes the text "Another file" into it.

Now, let's check the current ownership:

```bash
ls -lR new-dir 
```

`ls -lR` lists the contents of `new-dir` recursively. The `-R` option (recursive) makes `ls` list all files and subdirectories within `new-dir` and their contents.

You should see something like this:

```
new-dir:
total 4
-rw-rw-r-- 1 labex labex 13 Jul 29 09:15 file1.txt
drwxrwxr-x 2 labex labex 23 Jul 29 09:15 subdir

new-dir/subdir:
total 4
-rw-rw-r-- 1 labex labex 13 Jul 29 09:15 file2.txt 
```

![Screenshot 2568-02-14 at 8.22.47 AM.png](Permission%20Files%2019a778291991807c8ac7e1b6a0da3b62/Screenshot_2568-02-14_at_8.22.47_AM.png)

This shows that the directory `new-dir`, its subdirectory `subdir`, and the files `file1.txt` and `file2.txt` are all owned by `labex`.

Now, let's change the ownership of `new-dir` and all its contents to the `root` user:

```bash
sudo chown -R root:root new-dir 
```

In this command:

- The `R` option tells `chown` to operate recursively, changing the ownership of all files and subdirectories within `new-dir`. This is crucial; without `R`, only the `new-dir` directory's ownership would change, but the files and subdirectories within it would still be owned by `labex`.

Let's verify the change:

```bash
ls -lR new-dir 
```

You should now see:

```
new-dir:
total 4
-rw-rw-r-- 1 root root 13 Jul 29 09:15 file1.txt
drwxrwxr-x 2 root root 23 Jul 29 09:15 subdir

new-dir/subdir:
total 4
-rw-rw-r-- 1 root root 13 Jul 29 09:15 file2.txt 
```

![Screenshot 2568-02-14 at 8.25.26 AM.png](Permission%20Files%2019a778291991807c8ac7e1b6a0da3b62/Screenshot_2568-02-14_at_8.25.26_AM.png)

As you can see, the ownership of the directory and all its contents has changed to root. This demonstrates the power of the `-R` option for making widespread changes to ownership within a directory structure.

# **Changing the Permissions of a File**

In Linux, file permissions are represented by a series of letters or numbers. Let's explore how to read and change these permissions. Understanding permissions is vital for securing your files and preventing unauthorized access.

First, let's look at the current permissions of our `example.txt` file:

```bash
ls -l example.txt 
```

You might see something like this:

![Screenshot 2568-02-14 at 8.32.19 AM.png](Permission%20Files%2019a778291991807c8ac7e1b6a0da3b62/Screenshot_2568-02-14_at_8.32.19_AM.png)

```
-rw-rw-r-- 1 root root 0 Jul 29 15:11 example.txt 
```

The `-rw-rw-r--` part represents the file permissions. This is where the numeric and symbolic notations come in. Let's break it down:

- The first character (``) indicates this is a regular file. Other common indicators are `d` for directory and `l` for symbolic link.
- The next three characters (`rw-`) represent the owner's permissions (read and write, but not execute).
    - `r` stands for read permission: The owner can open and read the file.
    - `w` stands for write permission: The owner can modify the file.
    - `x` stands for execute permission: The owner can run the file (if it's a program or script). A `` means the permission is denied.
- The next three (`rw-`) are for the group. They have the same meaning as above, but apply to members of the file's group.
- The last three (`r--`) are for others (everyone else). They also have the same meaning, but apply to users who are neither the owner nor members of the file's group.

Now, let's change these permissions using the `chmod` command. `chmod` stands for "change mode," and it allows you to modify these permissions. We'll start with the **numeric notation**.

```bash
sudo chmod 700 example.txt 
```

In this command:

- `700` is a numeric representation of permissions:
    - The first digit (`7`) represents the owner's permissions.
    - The second digit (`0`) represents the group's permissions.
    - The third digit (`0`) represents the others' permissions.

Each digit is a number from 0 to 7, calculated by adding the values for read (4), write (2), and execute (1) permissions:

- `4`: Read permission
- `2`: Write permission
- `1`: Execute permission
- `0`: No permission

So, `7` (first digit) gives the owner read (4), write (2), and execute (1) permissions: 4+2+1=7

`0` (second digit) gives the group no permissions (0+0+0=0).

`0` (third digit) gives others no permissions (0+0+0=0).

Therefore, `700` means: Owner: read, write, execute. Group: none. Others: none.

Let's verify the change:

```bash
ls -l example.txt 
```

You should now see:

![Screenshot 2568-02-14 at 8.36.46 AM.png](Permission%20Files%2019a778291991807c8ac7e1b6a0da3b62/Screenshot_2568-02-14_at_8.36.46_AM.png)

```
-rwx------ 1 root root 0 Jul 29 15:11 example.txt 
```

The owner now has `rwx` (read, write, and execute) permissions, while the group and others have no permissions.

# **Changing the Permissions of a Directory**

Changing permissions for directories works similarly to changing permissions for files. Let's practice by creating a new directory and modifying its permissions. Directory permissions control who can list the directory's contents, create new files within the directory, and access files already in the directory.

First, let's create a new directory and set some non-standard permissions:

```bash
mkdir ~/test-dir
chmod 700 ~/test-dir 
```

Now, let's check the current permissions:

```bash
ls -ld ~/test-dir 
```

The `-d` option in `ls -l` tells `ls` to list the directory itself, rather than its contents. Without `-d`, `ls` would list the files and subdirectories *inside* `test-dir`, which is empty right now. You should see:

![Screenshot 2568-02-14 at 8.38.59 AM.png](Permission%20Files%2019a778291991807c8ac7e1b6a0da3b62/Screenshot_2568-02-14_at_8.38.59_AM.png)

```
drwx------ 2 labex labex 4096 Jul 29 15:45 /home/labex/test-dir 
```

The `d` at the beginning indicates that it's a directory. The `rwx------` indicates that the owner has read, write, and execute permissions, while the group and others have no permissions. For directories:

- Read permission (`r`) allows you to list the contents of the directory using `ls`.
- Write permission (`w`) allows you to create new files and subdirectories within the directory.
- Execute permission (`x`) allows you to access files and subdirectories within the directory (i.e., `cd` into it).

Now, let's change the permissions:

```bash
chmod -R 755 ~/test-dir 
```

In this command:

- `R` applies the change recursively to all files and subdirectories (though our directory is empty in this case). It's good practice to include it when dealing with directories, even if they're currently empty, in case you add files later.
- `755` gives read, write, and execute permissions to the owner, and read and execute permissions to group and others.

Let's break down `755`:

- Owner (7): Read (4) + Write (2) + Execute (1) = 7
- Group (5): Read (4) + Execute (1) = 5
- Others (5): Read (4) + Execute (1) = 5

Let's verify the change:

```bash
ls -ld ~/test-dir 
```

You should now see:

![Screenshot 2568-02-14 at 8.40.13 AM.png](Permission%20Files%2019a778291991807c8ac7e1b6a0da3b62/Screenshot_2568-02-14_at_8.40.13_AM.png)

```
drwxr-xr-x 2 labex labex 4096 Jul 29 15:45 /home/labex/test-dir 
```

This clearly shows the change in permissions, from only the owner having access (700) to the owner having full access while others can read and execute (755). Now, anyone can list the contents of `test-dir` and access files within it, but only the owner can create new files or modify existing ones.

# **Using Symbolic Notation for Permissions**

While numeric notation is concise, symbolic notation can be more intuitive, especially when you only want to change a single permission. Symbolic notation uses letters to represent the user, group, and others, and operators to add or remove permissions.

First, let's create a new script file with some content:

```bash
cd ~/project
echo '#!/bin/bash\necho "Hello, World"' > script.sh 
```

This command does two things:

1. It creates a new file named `script.sh`. The `.sh` extension is commonly used for shell scripts. shell scripts are executable files that contain a series of commands that are executed in sequence.
2. It writes two lines into this file:
    - `#!/bin/bash` (called a shebang) tells the system this is a bash script. The shebang line specifies the interpreter that should be used to execute the script. In this case, it's `/bin/bash`, which is the path to the Bash interpreter.
    - `echo "Hello, World"` is a command that will print "Hello, World" when the script runs. The `echo` command simply displays the text that follows it.
    - `\n` is a newline character, ensuring the commands are on separate lines in the file.

Now, let's check its initial permissions:

```bash
ls -l script.sh 
```

You should see something like:

![Screenshot 2568-02-14 at 8.42.00 AM.png](Permission%20Files%2019a778291991807c8ac7e1b6a0da3b62/Screenshot_2568-02-14_at_8.42.00_AM.png)

```
-rw-rw-r-- 1 labex labex 32 Jul 29 16:30 script.sh 
```

As you can see, initially, the script only has read and write permissions for the owner and group, and read permission for others. It doesn't have execute permission, which is required to run it as a program.

Let's try to run the script:

```bash
./script.sh 
```

You should see a "Permission denied" error because the script doesn't have execute permissions yet. The `./` part tells the shell to execute the script located in the current directory.

Now, let's add execute permission for the owner using **symbolic notation**:

```bash
chmod u+x script.sh 
```

In this command:

- `u` refers to the user (owner). Other options are `g` for group, `o` for others, and `a` for all (user, group, and others).
- `+x` adds execute permission. The `+` symbol adds a permission, while the `` symbol removes a permission.

So, `u+x` means "add execute permission for the owner."

Let's verify the change:

```bash
ls -l script.sh 
```

You should now see:

![Screenshot 2568-02-14 at 8.44.47 AM.png](Permission%20Files%2019a778291991807c8ac7e1b6a0da3b62/Screenshot_2568-02-14_at_8.44.47_AM.png)

```
-rwxrw-r-- 1 labex labex 32 Jul 29 16:30 script.sh 
```

The owner now has `rwx` (read, write, and execute) permissions.

Now, let's try running the script again:

```bash
./script.sh 
```

This time, you should see the output: "Hello, World"

This example clearly demonstrates why we need to add execute permissions to scripts, and the difference before and after adding these permissions. Symbolic notation makes it easy to modify specific permissions without having to recalculate the entire numeric representation.

# **Summary**

In this lab, we've explored essential Linux commands for managing file permissions:

1. We used `touch` to create new files and update existing ones.
2. We learned how to use `chown` to change file and directory ownership, including recursive changes for entire directory structures.
3. We practiced using `chmod` with both numeric and symbolic notation to modify file and directory permissions, understanding the different permission levels for owner, group, and others.
4. We saw practical examples of why permissions matter, such as needing execute permissions to run scripts.
5. We clarified the differences between numeric and symbolic notation for `chmod` and when each might be more appropriate.

These commands are crucial for maintaining security and controlling access in Linux systems. Remember to always be cautious when changing permissions, especially when using sudo, as incorrect changes can have significant consequences for system security and functionality. Always double-check your commands before executing them, and understand the implications of the changes you're making.