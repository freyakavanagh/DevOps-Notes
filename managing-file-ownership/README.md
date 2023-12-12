# Managing File Ownership

## Why is managing file ownership important?

Managing file ownership in Linux is crucial for security, access control, and accountability. It helps prevent unauthorized access, control permissions, and identify responsible users. Effective ownership management also facilitates group collaboration, resource management, and system administration tasks, contributing to an organized and secure file system.

## What is the command to view file ownership?

```ls -l [filename]```

## What permissions are set when a user creates a file or directory? Who does file or directory belong to?

Default Permissions:

For files: The default permissions are usually 666 (read and write for the owner, group, and others), and the umask value is subtracted from this. So, if the umask is 002, the default permissions for a new file would be 664.
For directories: The default permissions are typically 777 (read, write, and execute for the owner, group, and others), and the umask value is subtracted. Using the same umask of 002, the default permissions for a new directory would be 775.

Default Ownership:

The owner of the file or directory is the user who creates it. The user's default group becomes the group ownership of the file or directory.
For example, if the user "john" creates a file, the owner will be "john," and the group will be "john's default group."

## Why does the owner, by default, not recieve X permissions when they create a file?

When a user creates a new file, the default permissions are often set to allow read and write access for the owner (rw-). The assumption is that execute permissions are typically needed for programs or scripts, not for regular data files. Therefore, not granting execute permissions by default helps to limit the possibility of accidentally executing a data file as if it were a program.

## What command is used to change the owner of a file or directory?