# Bijoy Keyboard Layout Setup for Ubuntu Linux
![Ubuntu Logo](https://assets.ubuntu.com/v1/29985a98-ubuntu-logo32.png)

## 📝 Purpose
This repository provides a step-by-step guide and scripts to install and configure the Bijoy Keyboard Layout on Ubuntu Linux, enabling seamless Bangla typing with Bijoy Classic and Unicode layouts.

## Introduction
The Bijoy Keyboard Layout, developed by Mustafa Jabbar, is a popular choice for typing Bangla in Bangladesh. This guide helps you set up the Bijoy keyboard on Ubuntu using the IBus input method framework, ensuring compatibility with modern Ubuntu versions (e.g., 22.04, 24.04). It includes automation scripts and troubleshooting tips for a smooth experience.

---

## 1. Prerequisites
- **Ubuntu Version**: 20.04 LTS or later (tested on 22.04 and 25.04).
- **Internet Connection**: Required for downloading files and packages.
- **Administrative Privileges**: Sudo access for installing packages and modifying system files.
- **Required Files**: Download `bn-bijoyClassic.mim`, `bn-bijoyClassic.png`, `bn-bijoyUnicode.mim`, and `bn-bijoyUnicode.png` from [this GitHub repository](https://github.com/asikdial-tech/BijoyLinux) or the [releases page](https://github.com/your-username/bijoy-ubuntu-setup/releases).

---

## 2. Installation Steps
### Step 1: Update System and Install Dependencies
1. Open a terminal (`Ctrl + Alt + T`).
2. Update the package list and install required IBus packages:
   ```bash
   sudo apt update
   sudo apt install -y ibus-m17n m17n-db
   ```

### Step 2: Download and Place Bijoy Files
1. Download the Bijoy keyboard files:
   ```bash
   wget https://github.com/asikdial-tech/BijoyLinux/archive/refs/heads/main.zip
   unzip main.zip
   cd BijoyLinux-main
      unzip Bijoy/Linux.zip
      cd Bijoy/Linux

   ```
2. Move the files to the appropriate system directories:
   ```bash
   sudo chmod 777 /usr/share/m17n/
   sudo chmod 777 /usr/share/m17n/icons/
   sudo mv bn-bijoyClassic.mim /usr/share/m17n/
   sudo mv bn-bijoyClassic.png /usr/share/m17n/icons/
   sudo mv bn-bijoyUnicode.mim /usr/share/m17n/
   sudo mv bn-bijoyUnicode.png /usr/share/m17n/icons/
   ```

### Step 3: Update m17n-db Package List
1. Modify the `m17n-db` package list to include Bijoy files:
   ```bash
   sudo chmod 777 /var/lib/dpkg/info/m17n-db.list
   sudo nano /var/lib/dpkg/info/m17n-db.list
   ```
2. Append the following lines at the end of the file:
   ```
   /usr/share/m17n/icons/bn-bijoyClassic.png
   /usr/share/m17n/bn-bijoyClassic.mim
   /usr/share/m17n/icons/bn-bijoyUnicode.png
   /usr/share/m17n/bn-bijoyUnicode.mim
   ```
3. Save and exit (`Ctrl + O`, `Enter`, `Ctrl + X`).

### Step 4: Configure IBus Daemon
1. Add IBus to startup applications:
   - Go to **Settings > Startup Applications** (or search for “Startup Applications” in the application menu).
   - Click **Add** and enter:
     - **Name**: IBus Daemon
     - **Command**: `/usr/bin/ibus-daemon -d`
     - **Comment**: Start IBus daemon when GNOME starts
   - Click **Add** and close the window.
2. Alternatively, add it via terminal:
   ```bash
   gnome-session-properties
   ```
   Then add the same details as above.

### Step 5: Add Bijoy Keyboard Layouts
1. Open **IBus Preferences**:
   - Search for “IBus Preferences” in the application menu or run:
     ```bash
     ibus-setup
     ```
2. In the **Input Method** tab, click **Add**.
3. Select **Bengali** > **bijoyClassic (m17n)** and **bijoyUnicode (m17n)**, then click **Add**.
4. Close the window.

### Step 6: Restart System
Restart your system to apply changes:
```bash
sudo reboot
```

---

## 3. Using the Bijoy Keyboard
1. **Activate the Keyboard**:
   - Press `Ctrl + Space` to cycle through input methods.
   - Alternatively, use `Alt + Shift` to switch layouts.
2. **Test the Keyboard**:
   - Open an application like **LibreOffice Writer** (install with `sudo apt install libreoffice` if needed).
   - Select **bijoyClassic** or **bijoyUnicode** from the input method menu (top-right corner or IBus icon).
   - Start typing in Bangla. For example, typing `Zukta Ka` should produce the correct ligature if configured properly.

---

## 4. Automation Script
To simplify the setup, use the provided script (`install-bijoy.sh`) in the `scripts/` directory:
```bash
chmod +x scripts/install-bijoy.sh
./scripts/install-bijoy.sh
```
The script automates Steps 1–3. Manually complete Steps 4–5 after running it.

---

## 5. Troubleshooting
- **IBus not starting**: Ensure IBus is running:
  ```bash
  ibus-daemon -d
  ```
- **Keyboard layout not appearing**: Restart IBus:
  ```bash
  ibus restart
  ```
- **Permission issues**: Verify file permissions:
  ```bash
  ls -l /usr/share/m17n/
  ls -l /usr/share/m17n/icons/
  ```
- **Layout mismatch**: Confirm the correct layout is selected in IBus Preferences.
- **Further help**: Check [troubleshooting.md](docs/troubleshooting.md) or file an issue on this repository.

---

## 6. Conclusion
This guide sets up the Bijoy Keyboard Layout on Ubuntu for efficient Bangla typing. The included scripts and instructions ensure a quick and reliable setup. For feedback or contributions, visit the [GitHub repository](https://github.com/your-username/bijoy-ubuntu-setup).

### Contributing
Fork this repository, make improvements, and submit pull requests. Report issues or suggestions via the Issues tab.

### License
This project is licensed under the MIT License.
