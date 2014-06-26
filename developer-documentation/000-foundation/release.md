# Release

## Bundles

### Procedure

1. `git pull origin develop`
1. `git checkout -b release/<release>`
1. `grunt build`
1. `grunt publish`
1. Test the bundle manually
1. Update composer.json version
  * version property
  * sulu-bundles versions (bsp: 0.4.*)
1. `git commit`
1. `git commit`
1. `git checkout master``
1. `git merge --no-ff release/<release>`
1. `git branch -d release/<release>`
1. `git push origin master`
1. `git tag <release>` or tag the release on GitHub (especially if you want to mark it as development release)
1. `git checkout develop`
1. `git merge master`
1. Update composer.json depedencies
  * sulu-bundles dev-develop
  * version dev-develop (if it was before dev-develop)
1. `git push origin develop`
