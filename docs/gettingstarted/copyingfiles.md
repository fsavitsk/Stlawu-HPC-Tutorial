# Copying and Transferring Files

Transferring data between your local machine and the SLU HPC cluster is a fundamental task. Depending on your operating system and the size of your data, there are several tools available.

---

## Secure Copy Protocol (SCP)
SCP is a standard command-line utility for copying files and directories. It uses SSH for data transfer, providing the same security and authentication.

### SCP for Linux and macOS
Linux and macOS include SCP in the terminal by default. 

**Basic Syntax:**
`scp [source] [destination]`

* **Upload a file to the cluster:**
    ```bash
    scp /path/to/local/file.txt username@ada.hpc.stlawu.edu:/home/username/destination/
    ```
* **Download a directory from the cluster:**
    ```bash
    scp -r username@ada.hpc.stlawu.edu:/home/username/remote_folder ./local_destination/
    ```
    *(The `-r` flag stands for **recursive**, which is required for folders.)*

### SCP for Windows
* **PowerShell/CMD:** Modern Windows 10/11 includes native OpenSSH. You can use the exact same commands listed for Linux/macOS.
* **WinSCP:** A graphical (GUI) client. Best for users who prefer a drag-and-drop interface similar to Windows File Explorer.
* **Cygwin:** If using Cygwin to emulate a Linux environment, use the standard Linux `scp` syntax.

---

## Alternative Transfer Methods

### SFTP (Secure File Transfer Protocol)
SFTP is **interactive**. Unlike SCP, which is a one-off command, SFTP allows you to stay connected to browse and manage files.

1. **Connect:** `sftp username@ada.hpc.stlawu.edu`
2. **Upload:** `put local_file.txt`
3. **Download:** `get remote_file.txt`
4. **Exit:** `exit` or `bye`

### Rsync (Recommended for Large Data)
`rsync` is the most robust tool for large datasets or unstable connections. It synchronizes files and only copies the differences between the source and destination.

**Example Command:**
```bash
rsync -avz /local/directory/ username@ada.hpc.stlawu.edu:/home/username/remote_directory/
