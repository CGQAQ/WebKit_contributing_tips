# WebKit Contributing Tips

A practical guide to contributing to the [WebKit](https://webkit.org/) project. Whether you're a first-time contributor or an experienced developer, this guide covers the essential workflow from setup to submitting a pull request.

## Prerequisites

- macOS with [Xcode installed](https://webkit.org/build-tools/)
- Git

## Getting Started

### Clone the Repository

```bash
mkdir -p ~/code && cd ~/code
git clone https://github.com/WebKit/WebKit.git webkit
cd webkit
```

### Configure Git

```bash
git config core.fsmonitor true
git config pull.rebase true
```

### Add WebKit Scripts to PATH

Add the following line to your `~/.zshrc` so that WebKit helper scripts (e.g. `build-webkit`, `run-webkit-tests`) are available globally:

```bash
export PATH="$PATH:$HOME/code/webkit/Tools/Scripts"
```

> **Note:** If you skip this step, replace any script references with their full path, e.g. `./Tools/Scripts/build-webkit` instead of `build-webkit`.

### Set Up Your Environment

```bash
git webkit setup
```

### Update the Checkout

```bash
update-webkit
```

## Contributing Workflow

> See also: [WebKit Code Style Guidelines](https://webkit.org/contributing-code/#code-style-guidelines)

### 1. Make Your Changes

Write your code, then verify it conforms to WebKit's style:

```bash
check-webkit-style
```

### 2. Build

```bash
build-webkit --debug          # Debug build
build-webkit --release        # Release build
build-webkit --clean          # Remove build artifacts
```

To generate a compilation database for IDEs (VS Code, CLion, etc.):

```bash
build-webkit --export-compile-commands
```

### 3. Run Tests

```bash
run-webkit-tests [path/to/test]
```

| Flag | Description |
|------|-------------|
| `--reset-results` | Reset the expected test results |
| `--new-baseline` | Create a new baseline (equivalent to `--reset-results --add-platform-exceptions`) |

### 4. Import WPT Tests (if applicable)

Import [Web Platform Tests](https://web-platform-tests.org/) by directory:

```bash
import-w3c-tests web-platform-tests/css
```

> **Note:** Only directories are supported, not individual files.

### 5. Commit

Keep your changes in a **single commit**:

```bash
git add <files>
git commit
```

If you need to update the commit after further changes:

```bash
git commit --amend
```

Or squash multiple commits into one:

```bash
git webkit squash [--base-commit <hash>]
```

### 6. Submit a Pull Request

```bash
git webkit pull-request   # or: git webkit pr
```

On first run this creates a remote branch and opens a pull request. Subsequent runs push updates to the existing PR.

### 7. Check Out an Existing Pull Request

```bash
git webkit checkout <id>
```

Where `<id>` is a commit hash, branch name, or pull request reference (e.g. `pr-12345`).
