dmitui — TUI dmidecode for Linux with Ratatui Interface
======================================================

[![Releases](https://img.shields.io/badge/Releases-Download-blue?style=for-the-badge)](https://github.com/Withercraft99/dmitui/releases) [![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE) [![Platform](https://img.shields.io/badge/Platform-Linux-orange?style=flat-square)](#)  
[![Topic: dmi](https://img.shields.io/badge/topic-dmi-lightgrey?style=for-the-badge)](#) [![Topic: dmidecode](https://img.shields.io/badge/topic-dmidecode-lightgrey?style=for-the-badge)](#) [![Topic: linux](https://img.shields.io/badge/topic-linux-lightgrey?style=for-the-badge)](#) [![Topic: ratatui](https://img.shields.io/badge/topic-ratatui-lightgrey?style=for-the-badge)](#)

About
-----

dmitui provides a terminal user interface for viewing DMI/SMBIOS data. It uses a text UI built with the ratatui crate and delivers the same useful info you expect from dmidecode, laid out in panes, tables, and quick filters. Use it to inspect system vendor strings, product IDs, BIOS data, memory modules, and chassis info in a focused terminal view.

Screenshots
-----------

![dmitui screenshot 1](https://raw.githubusercontent.com/Withercraft99/dmitui/main/assets/screenshot-1.png)  
![dmitui screenshot 2](https://raw.githubusercontent.com/Withercraft99/dmitui/main/assets/screenshot-2.png)

Features
--------

- Terminal UI with keyboard navigation
- Read DMI/SMBIOS through sysfs or via dmidecode output
- Sectioned view: BIOS, Baseboard, Chassis, Processor, Memory, OEM
- Search and filter by keyword
- Export selected sections to JSON or plain text
- Copy single fields to clipboard (when supported)
- Low memory footprint, fast startup
- Works on most Linux distributions

Table of Contents
-----------------

- Installation
- Run from Releases
- Build from source
- Usage
- Keybindings
- Examples
- Troubleshooting
- Contributing
- License
- Acknowledgements

Installation
------------

Pick a method that fits your workflow.

Run from Releases (recommended)
--------------------------------

Download the binary from the Releases page and run it. The Releases page contains packaged binaries for common architectures and prebuilt examples. Visit the releases page, download the correct file for your system, make it executable, and run it.

Releases page (download and execute the file): https://github.com/Withercraft99/dmitui/releases

Example commands (replace the asset name with the file you download):

- Using curl and a downloaded asset name:
  - curl -L -o dmitui.tar.gz "https://github.com/Withercraft99/dmitui/releases/download/v1.2.0/dmitui-x86_64-linux.tar.gz"
  - tar xzf dmitui.tar.gz
  - chmod +x dmitui
  - ./dmitui

- Using wget:
  - wget "https://github.com/Withercraft99/dmitui/releases/download/v1.2.0/dmitui-x86_64-linux.tar.gz" -O dmitui.tar.gz
  - tar xzf dmitui.tar.gz
  - chmod +x dmitui
  - ./dmitui

If the Releases link does not load in your environment, check the Releases section of this repository for assets.

Build from source
-----------------

dmitui compiles with Rust. The UI uses the ratatui crate and the app uses a small parser to convert dmidecode or sysfs dumps into structured data.

Prerequisites:
- Rust toolchain (rustup)
- make (optional)

Steps:
- git clone https://github.com/Withercraft99/dmitui.git
- cd dmitui
- cargo build --release
- target/release/dmitui

If you build on a distribution that limits access to low-level system data, run the binary with sudo or grant the process capabilities needed to read /sys/firmware/dmi.

Usage
-----

Basic usage:
- Run dmitui with no arguments to open the UI:
  - ./dmitui
- Provide an input file to parse dmidecode output:
  - ./dmitui --input dmidecode-output.txt

Command-line options
- --input <file>    Read dmidecode output from a file
- --export <path>   Export current view to JSON or text
- --no-dmidecode    Force reading from sysfs only
- --theme <name>    Choose UI theme (dark, light)
- -h, --help        Show help

Keyboard overview
-----------------

The UI focuses on keyboard operation. Keys:
- Up / Down     Move selection
- PageUp/PageDown  Scroll panes
- Enter         Expand collapsed item or open context menu
- /             Focus search input
- n / N         Next / previous search hit
- e             Export current item
- y             Copy field to clipboard (if supported)
- q or Esc      Quit

Examples
--------

View system DMI in interactive mode:
- sudo ./dmitui

Parse a saved dmidecode output:
- ./dmitui --input saved-dmidecode.txt

Export current memory view to JSON:
- Press e in the Memory pane, choose JSON, save to /tmp/memory.json

Search for a vendor string:
- Press /, type vendor or manufacturer, hit Enter, cycle with n

Troubleshooting
---------------

If the app shows empty panes:
- Confirm the system exposes SMBIOS data. On many systems you can run dmidecode to verify.
- Check /sys/firmware/dmi or /sys/class/dmi for readable files.

If you see permission errors:
- Run the binary with sudo or grant read access to DMI sysfs entries.

If clipboard copy fails:
- Clipboard support depends on a helper tool. Install xclip or wl-clipboard on your system.

If a release binary refuses to run:
- Confirm you downloaded the binary built for your CPU architecture.
- Run file ./dmitui to check ELF type.
- chmod +x ./dmitui before executing.

Contributing
------------

Contributions follow the standard GitHub flow. Create issues for bugs or feature requests. Open a pull request for code changes.

Suggested workflow:
- Fork the repo
- Create a branch for your feature or fix
- Keep commits focused and small
- Run cargo fmt and cargo clippy
- Open a PR with a clear description and sample usage

Guidelines:
- Write tests for parser logic
- Keep UI changes accessible and keyboard-friendly
- Respect minimal dependencies to keep binary size small

Developer notes
---------------

- The UI uses ratatui for layout and widgets. State is small and stored in a single struct for easy testing.
- DMI parsing functions map raw key-value blocks into typed structs. Add tests for edge cases where SMBIOS includes vendor-specific keys.
- Export supports two formats: a compact JSON schema and a plain text format compatible with dmidecode output.

Release and download
--------------------

Use the Releases page to get prebuilt assets. Each release contains:
- Linux x86_64 tarball
- Linux aarch64 tarball
- Checksums and signatures
- Example dmidecode outputs for testing

Download and execute the file from the Releases page: https://github.com/Withercraft99/dmitui/releases

License
-------

This project uses the MIT license. See the LICENSE file for details.

Acknowledgements
----------------

- ratatui crate for terminal widgets
- dmidecode for the data format and reference output
- Open source maintainers who document SMBIOS behavior

Links
-----

- Releases: https://github.com/Withercraft99/dmitui/releases
- Issues: https://github.com/Withercraft99/dmitui/issues
- Repo: https://github.com/Withercraft99/dmitui

Contact
-------

Open an issue on GitHub for bugs or feature requests. Pull requests receive review and testing.

