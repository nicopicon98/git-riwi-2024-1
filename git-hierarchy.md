## Hierarchy of Git (configurations)

### 1. Local Configuration

- **Local Configuration** is specific to the repository.
- It is stored in the `.git/config` file in the repository.
- It can be set using the `git config` command with the `--local` option or by editing the `.git/config` file directly.

- **Example:**
  ```sh
  git config --local user.name "John Doe"
  ```

### 2. Global Configuration

- **Global Configuration** is specific to the user.
- It is stored in the `~/.gitconfig` file in the user's home directory.
- It can be set using the `git config` command with the `--global` option or by editing the `~/.gitconfig` file directly which is commonly located at `~/.config/git/config` or windows `C:\Users\<username>\.gitconfig`.

- **Example:**
  ```sh
  git config --global core.editor "nano"
  ```

### 3. System Configuration

- **System Configuration** is specific to the system.
- It is stored in the `/etc/gitconfig` file or in windows `C:\ProgramData\Git\config`.
- It can be set using the `git config` command with the `--system` option or by editing the `/etc/gitconfig` file directly or in windows `C:\ProgramData\Git\config`.

- **Example:**
  ```sh
  git config --system core.editor "code --wait"
  ```
