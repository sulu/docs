##![basic](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/basic.png)DET-102 Security

####Database Diagram

![Security database diagram](https://raw.github.com/massiveart/sulu-docs/master/detail-specification/images/db/security.png)

#####Description
Every Sulu user (which is just a special type of contact, but still has an own row in the the `se_users`-table, with a reference to the corresponding contact) can have some roles and groups.
The user-credentials (`username`, `password` containing a hash, and a `salt`, which is used to hash the password) are also stored in the `se_users`-table.

Roles define the permissions for a specific set of security context. These contexts are offered by different registered bundles in the Sulu system, and because of that the contexts are linked in the database as simple text-based keys. This information is stored in the `se_role`-table, additionally with the system and module which offers this security context. A system can also be described as a big section in Sulu, like Sulu itself, a shop or a community. The `module`-field can be used to group the contexts on an additional level, for instance the single bundles of a system.
The permission are stored as a bit field in a numeric data type in the `se_permissions`-table. This presentation is also used in the unix file systems. It is also supported by the Symfony Security Bundle, which makes it very easy to use this component.

Groups are stored in the `se_groups`-table, and they are simply a combination of some roles (which is resolved in the `co_group_roles`-table). They offer also the possibility to build a permission tree, which is again represented as a nested set (just like the accounts). On this way you can combine different permissions.

A Sulu user can be in several roles and several groups (stored in the tables `se_user_roles`and `se_user_groups`, and the combination of the resulting roles resp. permissions is the set of allowed operations for this specific user. 

####Authentication
Sulu uses the basic Symfony authentication as described in [this section of the symfony documentation](http://symfony.com/doc/current/book/security.html#how-security-works-authentication-and-authorization). A firewall is defined in the `app/config/security.yml`-file, which secures the `/admin`-url, where the sulu administration is located. The url `/admin/login` shows the login-form, and is of course also accessible when the user is not authenticated. The user provider is the `User`-model of our SecurityBundle, and as encoding `sha512` with 5000 iterations is used.
