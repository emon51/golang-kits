# Go CLI Commands – Beginner Friendly Guide

This document explains commonly used Go CLI commands and related Linux commands in a simple and clear way.

---

## 1. General Command Structure

```bash
go <command> [arguments/options]
```

* `go` → Go tool
* `<command>` → action (install, env, run, etc.)
* `[arguments/options]` → extra details

---

## 2. `go env GOPATH`

### Command:

```bash
go env GOPATH
```

### Explanation:

* `go` → Go CLI
* `env` → shows environment variables
* `GOPATH` → specific variable name

### Output Example:

```bash
/home/emon/go
```

### What is GOPATH?

A workspace directory where Go stores:

* `bin/` → installed binaries (e.g., bee)
* `pkg/` → compiled packages
* `src/` → source code (older usage)

---

## 3. `go env`

### Command:

```bash
go env
```

### Purpose:

Shows all Go environment variables.

### Common Variables:

* `GOPATH` → workspace path
* `GOROOT` → Go installation path
* `GOOS` → operating system
* `GOARCH` → CPU architecture

---

## 4. `go install`

### Command:

```bash
go install github.com/beego/bee/v2@latest
```

### Breakdown:

* `install` → download + build + install
* `github.com/beego/bee/v2` → module path
* `@latest` → latest version

### What it does:

1. Downloads the package
2. Compiles it
3. Creates a binary
4. Stores it in:

   ```bash
   ~/go/bin
   ```

---

## 5. PATH Configuration

### Command:

```bash
export PATH=$PATH:$(go env GOPATH)/bin
```

### Breakdown:

* `export` → set environment variable
* `PATH` → list of executable directories
* `$PATH` → current value
* `$(go env GOPATH)` → runs command and inserts result
* `/bin` → directory containing installed tools

### Purpose:

Allows running commands like `bee` from anywhere.

---

## 6. Check Installed Binaries

### Command:

```bash
ls ~/go/bin
```

### Purpose:

Lists installed Go tools.

---

## 7. Edit Shell Configuration

### Command:

```bash
nano ~/.bashrc
```

### Purpose:

Open shell configuration file to make permanent changes.

---

## 8. Reload Configuration

### Command:

```bash
source ~/.bashrc
```

### Purpose:

Apply changes without restarting terminal.

---

## 9. Check PATH Variable

### Command:

```bash
echo $PATH
```

### Purpose:

Displays all directories where the system looks for commands.

---

## 10. Summary Table

| Command           | Description                    |
| ----------------- | ------------------------------ |
| `go env`          | Show all environment variables |
| `go env GOPATH`   | Show Go workspace path         |
| `go install`      | Install Go package/tool        |
| `export PATH=...` | Add directory to PATH          |
| `ls`              | List files                     |
| `nano`            | Edit file                      |
| `source`          | Reload config                  |
| `echo $PATH`      | Show PATH directories          |

---

## Final Note

If a Go command like `bee` is not found after installation, it is usually because the binary directory (`~/go/bin`) is not added to your PATH.

Fixing PATH solves most issues related to Go CLI tools.
```bash
export PATH=$PATH:$(go env GOPATH)/bin
```
