# Learning in monorepo:

- Adding local package dependency using yarn -> needs to specify version otherwise it will fail
  - https://github.com/yarnpkg/yarn/issues/4878
- Structuring webpack and monorepo
  - https://medium.com/@Georgian/webpack-4-config-for-lerna-monorepo-using-babel-7-and-jest-8342c4ebc239
- Intro to monorepo, example 2 packages as library also with webpack
  - https://codeburst.io/monorepos-by-example-part-3-1ebdea7ccbea

# Update process

Example 1:
- When `orange` added a new function that is not used for main then committed it
- Since `main` is dependant on `orange`, when running `lerna changed`, both `orange` and `main` is subject to change for next release
- Since `lerna` mode is not independent, both packages are updated to same version (leaving other package to be the same version)
