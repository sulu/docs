# How to create a Pull Request

* Create the pull request as soon as possible.
* Mark the PR with [WIP] in the title when you work on it.
* Remove the [WIP] when you finished open tasks and the PR will be able to merge.
* Template is devided in two parts: Tasks (for developer), Informations (for reviewer)
* Tasks list can be extended for developer tasks
* Informations: Tests => if tests fail, add reason
* Informations: Fixed Tickets => Tickets to close after merge

## Structure
```
[short description]:

__Tasks:__

- [ ] test coverage
- [ ] gather feedback for my changes
- [ ] submit changes to the documentation
- [ ] ... <add your own tasks>


__Informations:__

| Q             | A
| ------------- | ---
| Bug fix?      | [yes|no]
| New feature?  | [yes|no]
| Tests pass?   | [yes|no => <WHY?>]
| Fixed tickets | [<WHICH?>|none]
| Doc           | [url to doc|none]
```

## Example

Create User Command:

__Tasks:__

- [ ] test coverage
- [ ] gather feedback for my changes
- [ ] submit changes to the documentation
- [ ] remove Request defaults
- [ ] fix #1


__Informations:__

| Q             | A
| ------------- | ---
| Bug fix?      | no
| New feature?  | yes
| Tests pass?   | no => __dependency__ https://github.com/sulu-cmf/sulu/pull/86
| Fixed tickets | #1 , #2
| Doc           | https://github.com/massiveart/sulu-docs/blob/master/developer-documentation/400-contacts/create-user.md
