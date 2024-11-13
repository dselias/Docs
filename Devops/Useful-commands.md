# Ncdu - Disk usage analizer

`ncdu` (NCurses Disk Usage) is a disk usage analyzer with an interactive, text-based user interface. It provides a quick and easy way to view and analyze disk space usage within directories and subdirectories, making it very useful for cleaning up storage or monitoring disk space usage.

## Navigating the Interface

- **Arrow Keys:** Use up/down to navigate files and directories.
- **Enter:** Expand the selected directory to show subdirectories.
- **`d`:** Delete the currently selected file or directory.
- **`q`:** Quit `ncdu`.

## Usage

1. **Without Arguments:** Running `ncdu` without arguments scans the current directory.
  ```bash
  ncdu
  ```
2. **With Directory Argument:** You can specify a directory to scan.
  ```sh
  ncdu /path/to/directory
  ```
