# How to create a Pull Request

* __Use a meaningfull name for the Pull Request__
* Create the pull request as soon as possible.
* Name the branch after the following format: (feature|bugfix|hotfix|enhancement)/[issue-number]-<description>
  * the issue number is optional, but should always be provided if there is an issue
* Add a label for the type of the PR (Feature, Bugfix, Hotfix, Enhancement)
* Add a label for the state of the PR
  * in progress if you are still working on the PR
  * review when it is reviewable
  * feedback if you have reviewed someone else's PR
  * alternatively you can also use the [waffle board](https://waffle.io/sulu-cmf/sulu)
* Template is devided in two parts: Tasks (for developer), Informations (for reviewer)
* Tasks list can be extended for developer tasks
* Informations: Tests => if tests fail, add reason
* Informations: Fixed Tickets => Tickets to close after merge
* Informations: BC Breaks

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
| Tests pass?   | [yes|no => <WHY?>]
| Fixed tickets | [<WHICH?>|none]
| BC Breaks     | [description]
| Doc           | [url to commit|none]
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
