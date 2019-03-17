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

# Output from lerna commands:

Lerna version skipping through version:

```bash
$ D:\GitProjects\monorepo\node_modules\.bin\lerna version
lerna notice cli v3.13.1
lerna info current version 1.0.3
lerna info Looking for changed packages since v1.0.3
? Select a new version (currently 1.0.3) Patch (1.0.4)

Changes:
 - @monorepo-test/apple: 1.0.3 => 1.0.4
 - @monorepo-test/main: 1.0.3 => 1.0.4
 - @monorepo-test/orange: 1.0.2 => 1.0.4

? Are you sure you want to create these versions? Yes
lerna info execute Skipping GitHub releases
lerna info git Pushing tags...
lerna success version finished
Done in 17.47s.
```

Testing since the latest release change: (this case there is a change in `apple` package)

```bash
$ yarn lerna run test --since
yarn run v1.12.3
$ D:\GitProjects\monorepo\node_modules\.bin\lerna run test --since
lerna notice cli v3.13.1
lerna info Looking for changed packages since v1.0.4
lerna info Executing command in 2 packages: "yarn run test"
lerna info run Ran npm script 'test' in '@monorepo-test/apple' in 0.4s:
$ echo 'apple' && exit 0
'apple'
lerna info run Ran npm script 'test' in '@monorepo-test/main' in 0.3s:
$ echo 'main' && exit 0
'main'
lerna success run Ran npm script 'test' in 2 packages in 0.7s:
lerna success - @monorepo-test/apple
lerna success - @monorepo-test/main
Done in 1.52s.
```
