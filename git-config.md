# git config

`git config` is a command-line tool that is used to set or get configuration variables that control all aspects of how Git behaves. These variables can be stored in three different configuration files:

1. **Local Configuration**: Specific to the repository.
2. **Global Configuration**: Specific to the user.
3. **System Configuration**: Specific to the system.

## Syntax

The basic syntax of the `git config` command is as follows:

```sh
git config [<file-option>] [<name> [<value>]]
```

Let's break down the components of the command:

- `file-option`: This is an optional parameter that specifies the configuration file where the configuration should be stored. It can be one of the following:
  - `--local`: Store the configuration in the repository-specific `.git/config` file.
  - `--global`: Store the configuration in the user-specific `~/.gitconfig` file.
  - `--system`: Store the configuration in the system-wide `/etc/gitconfig` file.

- `name`: The name of the configuration variable.

- `value`: The value to be assigned to the configuration variable. If the value has got spaces, it should be enclosed in double quotes. For example: git config --global user.name "Nicolas Picon Jaimes" .  If the value is not provided, the command will return the current value of the configuration variable.

## Examples

### 1. Set User Name Locally

Set the user name for the current repository:

```sh
git config --local user.name "John Doe"
```

### 2. Set Core Editor globally

Set the default text editor for Git:

```sh
git config --global core.editor "nano"
```

### 3. Set Core Editor System-wide

Set the default text editor for Git system-wide:

```sh
git config --system core.editor "code --wait"
```

## 4. Get Configuration Value

`git config variable-name` can be used to get the value of a configuration variable:

Get the value of a configuration variable:

```sh
git config user.name
```

## 5. List All Configuration Variables and Values locally

List all the configuration variables along with their values:

```sh
git config --local --list
```