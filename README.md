# WebKit_contributing_tips

This document provides tips and guidelines for contributing to the WebKit project. Whether you're a first-time contributor or an experienced developer, these tips will help you navigate the contribution process effectively.

## Prerequisites
This guide assumes you have:
- macOS with Xcode installed [official guide](https://webkit.org/build-tools/)
- Git installed

## Getting Started
### Getting the Source Code
```bash
mkdir -p ~/code/
cd ~/code/
git clone https://github.com/WebKit/WebKit.git webkit
cd webkit

# make git faster with fsmonitor
git config core.fsmonitor true
git config pull.rebase true


# Set Scripts path for WebKit.
# Put it in your ~/.zshrc (recommended).
# If you don't want to add it to ~/.zshrc,
# the 'git webkit` should be all replaced by
# './Tools/Scripts/git-webkit', and all scripts
# should be replaced by './Tools/Scripts/[script-name]'
export PATH=$PATH:$(pwd)/Tools/Scripts
```

### Update the checkout
```bash
update-webkit
```

### Setting Up Your Environment

```bash
git webkit setup
```


## Starting to Contribute
### Check code style after you done your changes
```bash
check-webkit-style
```
### Build WebKit
```bash
# for Debug build
build-webkit --debug
# for Release build
build-webkit --release

# clean up build artifacts
build-webkit --clean

# you can generating compilation database for IDEs like VSCode or CLion
build-webkit --export-compile-commands
```
### Run tests
```bash
run-webkit-tests [path/to/test]

# use --reset-results to reset the test results
run-webkit-tests --reset-results [path/to/test]

# use --new-baseline to create a new baseline for the test results
# equivalent to --reset-results --add-platform-exceptions
run-webkit-tests --new-baseline [path/to/test]
```

### Import WPT
```bash
# only directory is supported, not individual files
import-w3c-tests [web-platform-tests/[dir path in wpt]]

# for example, to import all tests in css
import-w3c-tests web-platform-tests/css
```

### Finally commit your changes
```bash
git add [files you changed]
git commit

# you should always keep your changes in a single commit, so if you need to make changes after the commit, use amend
git commit --amend

# or you can squash your commits into one commit before pushing
git webkit squash [--base-commit [base-commit-hash]]
```

### Lastly push your changes
```bash
# if you are first time running this, it will create a branch, upload and create a pull request for you; if not, it will just push to the branch and update the pull request
git webkit pull-request
# or in short
git webkit pr
```

### You can also checkout a existing pull request and continue working on it
```bash
# id should be string representation of a commit, branch or pull request (pr-#) to apply locally
git webkit checkout [id]
```
