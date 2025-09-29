# Users and Groups
Linux uses a system of users and groups to handle access control. Each user has a unique numeric UID and an associated user name. Users can be added to groups, which have a unique numeric GID and name.

## Users

In Linux, users form the foundation for isolating and securing system files and resources. Every process runs under a user identity (UID), and by default only the process owner or root can control or interact with it.
Linux does not categorise different user types, but in practice they can be considered either **interactive** or **service** users. **Interactive** accounts are intended to be used by humans logging onto the machine to run applications. They usually have access to a shell, or a GUI session on systems that have one. **Service** users are non-login accounts that run background processes (daemons) with restricted priviliges.

On modern distributions, it is the convention to assign interactive users UIDs that start at 1000. Service users are given UIDs between 1 and 999. This is not mandatory, but it is a recommended best practice. The root user is always given UID 0.

## Groups

In addition to users, Linux has groups, which are used to manage permissions collectively. Groups are identified by a unique name and numeric group ID (GID).

Each user must be in at least one group. By default, a group is created for the user when the user is created, with the group name and GID matching the user name and UID (as long as the GID is available).

Users can be members of multiple groups. Groups that are not the user's primary group are called secondary groups. This allows resources to be shared between groups of users.

Group IDs follow the same numbering convention as user IDs - service groups use 1-999, interactive groups use 1000+, and the root group uses GID 0.

