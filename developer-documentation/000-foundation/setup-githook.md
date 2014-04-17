#Setup for git hooks
To setup the git hooks for example to make a build before each push execute following after cloning the repository (grunt needed):
```
grunt install:hooks
```

Currently this will add a pre-push hook which will be executed before each push and it will execute the grunt-build-task before pushing everything to the repo.
