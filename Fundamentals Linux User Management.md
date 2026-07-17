User Management is one of the **most important skills** for a Linux System Administrator. Every Linux server, whether it's a web server, database server, cloud VM, or enterprise infrastructure, depends on proper user and permission management.

## ***Fundamentals***

1. What is a user?

A **user** is an identity that represents a person, service, or application that can log in to and use a computer system. In Linux, every action is performed by a user account.

Users help Linux:

- Keep files private
- Control who can access what
- Improve security
- Allow multiple people to use the same system safely
- Track who performed specific actions

2.  What is a group?

A **group** is a collection of one or more users in Linux that share the same permissions and access rights to files, directories, and system resources.

Instead of assigning permissions to each user individually, Linux allows administrators to assign permissions to a **group**, making user and permission management simpler and more efficient.

Groups are used to:

- Simplify permission management.
- Allow multiple users to share resources.
- Reduce administrative overhead.
- Improve security through controlled access.
- Support collaborative work environments.

3. What is UID (User ID)?

A **UID (User ID)** is a **unique numeric identifier** assigned to every user account in Linux. The operating system uses the UID—not the username—to identify users and determine file ownership, permissions, and process privileges.

Although humans use usernames like `sajib` or `alice`, Linux internally uses the **UID**.

