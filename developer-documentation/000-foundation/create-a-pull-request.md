#How to create a Pull Request

* Create the pull request as soon as posible.
* Mark the PR with [WIP] in the title when you work on it.
* Remove the [WIP] when you finished open tasks and the PR will be able to merge.

##Structure
```
[short description]:

- [ ] test coverage
- [ ] finish the code
- [ ] gather feedback for my changes
- [ ] submit changes to the documentation


| Q             | A
| ------------- | ---
| Bug fix?      | [yes|no]
| New feature?  | [yes|no]
| Tests pass?   | [yes|no|none]
| Fixed tickets | [yes|no|none]
| Doc           | [url to doc|none]
```

##Example
Create User Command:

- [x] test coverage (no tests)
- [x] finish the code
- [ ] gather feedback for my changes
- [x] submit changes to the documentation


| Q             | A
| ------------- | ---
| Bug fix?      | no
| New feature?  | yes
| Tests pass?   | none
| Fixed tickets | none
| Doc           | https://github.com/massiveart/sulu-docs/blob/master/developer-documentation/400-contacts/create-user.md
