# Logging into the Cluster

To access the SLU HPC cluster, you must use **SSH (Secure Shell)**. This provides an encrypted tunnel to the head node, where you can manage files and submit jobs.

---

## Standard SSH Connection

### Linux and macOS
SSH is built directly into the terminal of these operating systems.
1. Open your **Terminal** application.
2. Run the following command:
   ```bash
   ssh username@hpc.stlawu.edu
   ```
3. Enter your ada password when prompted. (Note: 1. the first time logging in you will need to set a new password after using your temp. 2. The cursor will not move while you type your password.)

### Windows
**PowerShell / Command Prompt:** Modern Windows (10/11) includes a native SSH client. You can use the same 'ssh username@hpc.stlawu.edu' command listed above.
**PuTTY:** A classic standalone SSH client. Download it from the PuTTY website.
**Cygwin:** Provides a Linux-like environment for Windows. If you have Cygwin installed, use the standard Linux SSH syntax.

## Visual Studio Code (VS Code) SSH (Recommended)
Using VS Code is highly recommended as it provides a Graphical User Interface (GUI) for editing files directly on the cluster.
### Setup steps
1. **Install Remote Development Extension:** Open VS Code, go to the Extensions view (Ctrl+Shift+X), and install the "Remote - SSH" extension by Microsoft.
2. **Connect to the Cluster:**
   - Click the Remote Window icon (a small green or blue icon in the bottom-left corner).
   - Select Connect to Host... > Add New SSH Host....
   - Enter: 'ssh username@hpc.stlawu.edu'.
   - Select your SSH configuration file (usually the first option in '/Users/yourname/.ssh/config').
3. **Open a Folder:** Once connected, you can go to File > Open Folder to browse your home directory on the cluster just like a local folder.

## Passwordless SSH (SSH Keys)
Tired of typing your password? You can set up SSH keys to log in automatically and securely.

1. **Generate a Key Pair**
   On your local machine, run:
   ```bash
   ssh-keygen
   ```
   Press Enter through all prompts (do not set a passphrase if you want truly automatic login).
   **Note:** If you already have an existing key pair you can just use that, however for security purposes it is not reccomended as best practice and you should use a seperate key pair for every ssh service you use.
2. **Copy the Key to the Cluster** Use the ssh-copy-id utility to send your public key to the cluster:
   ```bash
   ssh-copy-id username@hpc.stlawu.edu
   ```
   After this, you will no longer be prompted for a password when logging in from that specific computer.

## SSH key doesnt work
If you find yourself still having to enter your password to login instead of it using your ssh key then you may need to edit your ssh config file.

You will have to edit the config and specify your key file and connection, this is needed if you created a new key with a new name.

Now you are logged in, congrats! Check out the doumentation and tutorials for using commands and running jobs.
