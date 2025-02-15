# User Account Management

Welcome to the lab "User Account Management".

# **Introduction**

This lab will guide you through basic user account management operations in Linux systems. You'll learn how to create, modify, and delete user accounts, as well as how to set and change passwords. These are fundamental skills for Linux system administration. Don't worry if you're new to Linux - we'll explain everything step by step!

# **Creating a New User**

Let's start by creating a new user account named "joker".

1. Open a terminal. In Linux, the terminal is a text interface where you can enter commands.
2. Type the following command and press Enter:

```bash
sudo useradd joker 
```

Let's break this down:

- `sudo` is a command that gives you temporary superuser (administrator) privileges. We use it because creating a new user requires these higher-level permissions.
- `useradd` is the command to create a new user.
- `joker` is the username we're creating.

Note: If you try to run this command without `sudo`, you'll get a "permission denied" error. This is because regular users aren't allowed to create new user accounts - it's a task reserved for system administrators.

This highlights the difference between a superuser and a common user. As a common user, you can't create new user accounts, but by using `sudo`, you can temporarily elevate your privileges to perform this administrative task.

1. To verify that the user was created, we'll examine the `/etc/passwd` file:

```bash
sudo grep -w 'joker' /etc/passwd 
```

The `/etc/passwd` file is like a phonebook for user accounts. Each line represents one user account, with different pieces of information separated by colons (:).

You should see output similar to:

![Screenshot 2568-02-15 at 1.32.22 PM.png](User%20Account%20Management%2019b778291991809bae5ef98f03564b7c/Screenshot_2568-02-15_at_1.32.22_PM.png)

```
joker:x:5001:5001::/home/joker:/bin/sh 
```

This line shows:

- Username: joker
- Password: x (the actual password is stored securely elsewhere)
- User ID: 5001
- Group ID: 5001
- Home Directory: `/home/joker`, but it hasn't been created yet
- Default Shell: `/bin/sh`

# **Creating a User with a Home Directory**

Now, let's create another user named "bob" and give them a home directory.

1. Run the following command:

```bash
sudo useradd -m bob 
```

The `-m` option tells the system to create a home directory for the user. A home directory is like a personal folder where a user can store their files and settings.

1. Let's verify that the home directory was created:

```bash
sudo ls -ld /home/bob 
```

You should see output similar to:

![Screenshot 2568-02-15 at 1.35.44 PM.png](User%20Account%20Management%2019b778291991809bae5ef98f03564b7c/Screenshot_2568-02-15_at_1.35.44_PM.png)

```
drwxr-x--- 2 bob bob 57 Jan 19 13:33 /home/bob 
```

This output shows:

- `d` at the start means it's a directory
- `rwxr-x---` shows who can read, write, or execute in this directory
- The two `bob` entries show that both the user and group owner of this directory is bob
- `57` is the size of the directory in bytes
- `Jan 19 13:33` is when the directory was created
- `/home/bob` is the location of the directory

# **Setting a User Password**

Now we need to set a password for our new users. Let's set a password for "joker".

1. Run the following command:

```bash
sudo passwd joker 
```

1. You'll be asked to enter a new password twice. For this lab, use a simple password like "password123".

The password will not be displayed as you type it. This is a security feature to prevent others from seeing your password as you type it.

Important: Remember this password! You'll need it later in the lab.

1. If successful, you'll see a message saying "passwd: password updated successfully".
    
    ![Screenshot 2568-02-15 at 1.38.04 PM.png](User%20Account%20Management%2019b778291991809bae5ef98f03564b7c/Screenshot_2568-02-15_at_1.38.04_PM.png)
    

Note: In a real-world scenario, always use strong, unique passwords!

Behind the scenes, Linux stores encrypted passwords in a secure file called `/etc/shadow`. This is more secure than storing them in the `/etc/passwd` file where anyone could see them.

# **Modifying User Properties**

Linux allows us to change various settings for a user account after it's been created. Let's change joker's home directory as an example.

1. Run the following command:

```bash
sudo usermod -d /home/shiyanlou joker 
```

Here's what this does:

- `usermod` is the command to modify user account settings
- `d /home/shiyanlou` specifies the new home directory
- `joker` is the user we're modifying
1. Let's verify the change:

```bash
sudo grep -w 'joker' /etc/passwd 
```

- `w` is used to match the whole word, and `grep` is used to search for the word in the file. You should see that joker's home directory has been updated in the output.
    
    ![Screenshot 2568-02-15 at 1.40.43 PM.png](User%20Account%20Management%2019b778291991809bae5ef98f03564b7c/Screenshot_2568-02-15_at_1.40.43_PM.png)
    

# **Changing User Shell**

Another important setting we can modify is the user's default shell. The shell is the program that interprets and runs the commands you type in the terminal.

By default, the user 'joker' is using `/bin/sh` as their shell. While `sh` (Bourne Shell) is a basic shell that's present on most Unix-like systems, `bash` (Bourne Again Shell) offers more features and is generally more user-friendly.

Changing joker's shell to bash provides several benefits:

- More intuitive command-line interface
- Enhanced scripting capabilities
- Better customization options for the user's environment

Here's how to make the change:

1. Change joker's default shell to bash:

```bash
sudo usermod -s /bin/bash joker 
```

1. Verify the change:

```bash
sudo grep -w 'joker' /etc/passwd 
```

You should see `/bin/bash` at the end of joker's entry. This means bash is now joker's default shell.

![Screenshot 2568-02-15 at 1.46.06 PM.png](User%20Account%20Management%2019b778291991809bae5ef98f03564b7c/Screenshot_2568-02-15_at_1.46.06_PM.png)

After making this change, joker will have access to the more feature-rich bash environment whenever they log in or open a new terminal session.

# **Adding a User to a Group**

In Linux, we use groups to organize users and manage permissions. One important group is the `sudo` group, which gives users administrative privileges. Let's add joker to the `sudo` group as an example.

Why would we add a user to the sudo group?

1. System administration: Users in the sudo group can perform system-wide administrative tasks.
2. Software installation: Sudo group members can install and update software packages.
3. Configuration changes: They can modify system configuration files.
4. User management: They can create, modify, or delete other user accounts.

You might wonder: "Why add someone to the sudo group when we can always use the 'sudo' command?" Here's why:

- Convenience: Users in the sudo group can use sudo without needing to know the root password. They use their own password instead.
- Granular control: System administrators can configure sudo to allow specific users to run only certain commands with superuser privileges.
- Accountability: Unlike sharing the root password, sudo logs who ran what command, improving security and traceability.
- Security: It's generally more secure to have named accounts with sudo access than to share the root password among multiple admins.

In a real-world scenario, you would typically add a user to the sudo group if:

- They are a system administrator or IT staff member who needs to perform regular maintenance tasks.
- They are a developer who needs to install specific software or make system changes for their work.
- They are a power user who needs elevated privileges for certain tasks, but you don't want to give them the root password.

Remember, adding a user to the sudo group gives them significant power over the system, so this should be done cautiously and only when necessary.

Now, let's add joker to the sudo group:

1. Run this command:

```bash
sudo usermod -aG sudo joker 
```

Here's what this does:

- `usermod` is the command to modify user accounts
- `aG` means "append to Group" (add to a group without removing from other groups)
- `sudo` is the group we're adding the user to
- `joker` is the user we're modifying
1. Verify the change:

```bash
groups joker 
```

You should see `sudo` listed among joker's groups.

1. To see the effect of this change, we need to switch to the joker user and try a command that requires sudo privileges:
    
    ![Screenshot 2568-02-15 at 1.50.42 PM.png](User%20Account%20Management%2019b778291991809bae5ef98f03564b7c/Screenshot_2568-02-15_at_1.50.42_PM.png)
    

```bash
su - joker 
```

This command switches from your current user (labex) to the joker user. You will be prompted to enter joker's password. Remember, this is the password you set earlier (`password123`). As you type the password, you won't see any characters on the screen - this is a security feature.

1. Once logged in as joker, let's try to view a file that normally requires root privileges:

```bash
sudo cat /etc/shadow 
```

Enter joker's password again when prompted. You should be able to see the contents of the `/etc/shadow` file, which is usually only accessible to root. This confirms that joker now has sudo privileges.

1. After you're done, type `exit` to return to your original user account (labex).

Note: In a production environment, you should be very careful about who you add to the sudo group. With great power comes great responsibility!

# **Locking and Unlocking User Accounts**

Sometimes, you might need to temporarily disable a user account without deleting it.

1. Lock the joker account:

```bash
sudo passwd -l joker 
```

The `-l` option locks the password.

1. Try to switch to the joker user:

```bash
su - joker 
```

You'll be asked for a password. Enter the password you set for joker earlier ("password123" if you followed our suggestion).

You should see an "authentication failure" message. This means the account is successfully locked.

![Screenshot 2568-02-15 at 1.58.23 PM.png](User%20Account%20Management%2019b778291991809bae5ef98f03564b7c/Screenshot_2568-02-15_at_1.58.23_PM.png)

1. Now, let's unlock the account:

```bash
sudo passwd -u joker 
```

The `-u` option unlocks the password.

1. Try switching to the joker user again:

```bash
su - joker 
```

Enter the password when prompted. This time, you should be able to switch to the joker user successfully.

![Screenshot 2568-02-15 at 2.00.38 PM.png](User%20Account%20Management%2019b778291991809bae5ef98f03564b7c/Screenshot_2568-02-15_at_2.00.38_PM.png)

**Type `exit` to return to your original user account before continuing to the next step.**

# **Deleting a User**

Finally, let's learn how to delete a user. We'll delete the "bob" user we created earlier.

1. Delete bob and their home directory:

```bash
sudo userdel -r bob 
```

The `userdel` command deletes user accounts. The `-r` option removes the user's home directory and mail spool.

1. Verify that the user has been deleted:

```bash
sudo grep -w 'bob' /etc/passwd
sudo ls -ld /home/bob 
```

Both commands should return no results. This means the user and their home directory have been successfully removed.

# **Summary**

Congratulations! You've completed the Linux User Account Management lab. You've learned how to:

1. Create new user accounts
2. Set user passwords
3. Modify user properties like home directory and default shell
4. Add users to groups
5. Lock and unlock user accounts
6. Delete user accounts

You've also been introduced to important Linux concepts like the `/etc/passwd` file, home directories, shells, and user groups. These are fundamental skills for Linux system administration. Remember, in real-world scenarios, always follow your organization's security policies when managing user accounts.