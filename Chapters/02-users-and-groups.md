# Users and Groups
Linux uses a system of users and groups to handle access control. Each user has a unique numeric UID and an associated user name. Users can be added to groups, which have a unique numeric GID.

## Users

In Linux, users form the foundation for isolating and securing system files and resources. Every process runs under a user identity (UID), and by default only the process owner or root can control or interact with it.
Linux does not categorise different user types, but in practice they can be considered either **interactive** or **service** users. **Interactive** accounts are intended to be used by humans logging onto the machine to run applications. They usually have access to a shell, or a GUI session on systems that have one. **Service** users are non-login accounts that run background processes (daemons) with restricted priviliges.

On modern distributions, it is the convention to assign interactive users UIDs that start at 1000. Service users are given UIDs between 1 and 999. This is not mandatory, but it is a recommended best practice. The root user is always given UID 0.