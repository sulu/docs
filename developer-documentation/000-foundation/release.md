# Release

## Bundles

### Procedure

1. `git pull origin develop`
1. `git checkout -b release/<release>`
1. `grunt build`
1. `grunt publish`
1. Test the bundle manually
1. `git commit`
1. Update composer.json version
1. `git checkout develop``
1. `git merge --no-ff release/<release>`
1. `git branch -d release/<release>`
1. `git push origin develop`
1. `git checkout master`
1. `git merge develop`
1. `git push origin master``
1. `git tag <release>` or tag the release on GitHub (especially if you want to mark it as development release)
