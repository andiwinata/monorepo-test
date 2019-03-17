# Learning in monorepo:

- Adding local package dependency using yarn -> needs to specify version otherwise it will fail
  - https://github.com/yarnpkg/yarn/issues/4878
- Structuring webpack and monorepo
  - https://medium.com/@Georgian/webpack-4-config-for-lerna-monorepo-using-babel-7-and-jest-8342c4ebc239
- Intro to monorepo, example 2 packages as library also with webpack
  - https://codeburst.io/monorepos-by-example-part-3-1ebdea7ccbea

# Update process

Example 1:
- All packages start with v1.0.1
- When `orange` added a new function that is not used for main then committed it
- Since `main` is dependant on `orange`, when running `lerna changed`, both `orange` and `main` is subject to change for next release
- Since `lerna` mode is not independent, both packages are updated to same version (leaving other package to be the same version)

Example 2:
- Packages start with v1.0.2 for `main` and `orange`
- `apple` is still in v1.0.1
- Now, change something in `apple` package and then commit it
- `lerna changed` will say both `main` and `apple` are changed
- `lerna version` will bump both `main` and `apple` to v1.0.3 (`apple` skips through v1.0.2, and leave `orange` still at v1.0.2
