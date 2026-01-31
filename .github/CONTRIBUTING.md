# Contributing to vfio-windows-aio | script

Thank you for your interest in improving `vfio-windows-aio` script!

Given the nature of this project (kernel modules, hardware passthrough, VM management), we prioritize **safety** and **reliability**.

## ⚠️ Safety First

**This script interacts with hardware at a low level.** Improper configuration can lead to system instability, data loss, or (in extremely rare cases) hardware damage.

*   **Test on your own hardware first.** Do not submit anything that you haven't verified (for the sake of us all)
*   **Backup your data.** Crucial step, do not lose your data because of some random script on the internet.
*   **Be explicit.** If a change involves a risk, document it clearly in the comments and the PR description.

## Reporting Bugs

We appreciate bug reports! However, please understand that VFIO setups are very highly hardware-dependent. What works on a ThinkPad P53 might not work on a custom desktop.

### What to Include in a Bug Report
1.  **Hardware Specifications**: CPU, GPU, Motherboard/Laptop Model.
2.  **OS / Kernel Version**: `uname -r`, Distribution name.
3.  **Logs**: Output of the script, `dmesg` (relevant parts or something that caught your eye), and `/var/log/libvirt/qemu/[vm-name].log`.
4.  **IOMMU Groups**: Output of your IOMMU grouping script or `lspci -nn`.

## 🛠️ Development Guidelines

### Shell Scripting
This project relies mainly on bash. Please adhere to the following:

*   **Indentation**: Use **4 spaces**. Do not use tabs.
*   **Shebang**: Maintain `#!/bin/bash` at the top.
*   **Root Checks**: If a command requires root, ensure the script handles permissions or checks for `sudo`.
*   **Error Handling**: Check for the existence of files (like `/sys/...`) before writing to them.
    ```bash
    if [ -e "/path/to/virtual/file" ]; then
        echo "1" > /path/to/virtual/file
    fi
    ```
*   **Comments**: Comment liberally. VFIO logic can be obscure; explain *why* you are doing something, not just *what*.

### Tools
*   **ShellCheck**: I recommend running `shellcheck` on your changes to catch common mistakes.
    ```bash
    shellcheck start_vm.sh
    ```

## 📥 Pull Request Process

1.  **Fork** the repository.
2.  **Create a branch** for your feature or fix: `git checkout -b fix/nvidia-driver-reload`.
3.  **Test** your changes thoroughly.
4.  **Commit** with clear messages.
5.  **Push** and open a **Pull Request**.

### PR Description
In your PR, describing:
*   **The Problem**: What are you fixing or adding?
*   **The Solution**: How did you implement it?
*   **Verification**: **Crucial.** Describe the hardware you tested this on and the results.

## 📄 License

It's MIT! You can do whatever you want with it, just don't blame me if something breaks. I am not responsible for any damage you may cause to your system. You are on your own. Sorry :C
