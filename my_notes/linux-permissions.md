Linux File Permissions and Ownership Mastery
============================================

Subject
-------

Linux System Administration

Topics Covered
--------------

*   Octal and Symbolic Permission Notations
    
*   File and Group Ownership Management (`chown`, `chgrp`)
    
*   Special Permission Bits (SetUID, SetGID, Sticky Bit)
    
*   Umask and Default Permissions Calculation
    

💡 Summary
----------

This study guide summarizes the core principles of Linux file access control, which is critical for system security and management. It covers how to read and assign permissions using both the numerical (octal) and symbolic notations, how to manage the user and group responsible for a file, and the functions of advanced special permissions like SetUID, SetGID, and the Sticky Bit. Finally, it reinforces how the system's default permission setting is calculated using the umask value.

🧠 Key Concepts
---------------

*   **Octal Permission System (R/W/X):** The numerical foundation where Read (`r`)=4, Write (`w`)=2, and Execute (`x`)=1. Permissions are always calculated by summing these values for the three categories: Owner, Group, and Others (e.g., `rwxr-xr--` is 4+2+1, 4+0+1, 4+0+0, resulting in **754**).
    
*   **Symbolic Notation (u/g/o/a, +/-/=, r/w/x):** A flexible method for modifying permissions. Users are categorized as Owner (u), Group (g), Others (o), or All (a). Permissions are Added (+), Removed (-), or Exactly Set (=) (e.g., chmod go+x).
    
*   **SetUID (SUID) Bit:** Represented by a leading 4 in the four-digit octal notation (e.g., 4755) or a lowercase s in the owner's execute position (-rws...). When set on an executable file, it allows any user executing the file to run it with the **permissions of the file's owner**.
    
*   **Sticky Bit (t or T):** Represented by a leading 1 in the four-digit octal notation. When applied to a directory (like /tmp), it ensures that users can only delete or rename files within that directory if they are the file's owner (or the root user), even if they have write permission on the directory.
    
*   **Umask:** A configuration value (e.g., 0022) that defines the default permissions for newly created files and directories. The umask is a _mask_ of bits to be **removed** from the maximum base permissions (777 for directories, 666 for files). Resulting permissions are: Base - Umask.
    

📚 Vocabulary List
------------------

*   chmod: The command used to **change the access mode** (permissions) of a file system object.
    
*   chown: The command used to **change the user owner** and/or the **group owner** of a file or directory. Syntax is typically chown user:group file.
    
*   chgrp: The command used specifically to **change the group owner** of a file or directory.
    
*   Owner (u): The user who owns the file, controlling the first set of three permission bits.
    
*   Group (g): The group associated with the file, controlling the second set of three permission bits.
    

❓ Key Questions for Review (Active Recall)
------------------------------------------

*   How do directory permissions differ from file permissions (e.g., what is required to enter vs. read vs. create a file)?
    
*   How would you use the chown command to recursively change the ownership of a directory and all its contents to a new user and group?
    
*   Explain the difference in meaning between an s and a capital S in the permission string (e.g., in the owner's position).
    
*   If the system's umask is set to 0007, what permissions will a newly created directory have by default?