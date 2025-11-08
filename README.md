# Tecno Spark 10 (KI5q) Ultimate Rooting Guide

This is a step-by-step guide to achieve **Systemless Root** access on your Tecno Spark 10 (KI5q) using the **Fastboot method** and **Magisk**.

---

## ⚠️ Critical Warnings: READ FIRST!

| Caution | Description |
| :--- | :--- |
| **Data Wipe** | **Unlocking the bootloader will factory reset your device and erase ALL data.** Back up everything important (photos, contacts, app data) before starting. |
| **Responsibility** | i am not responsible for any damage dealt to your device although it is very unlikely if you do every step correctly and Rooting Your device And Unlocking the bootloader will wipe ALL data on your phone. Ensure you have backed up everything important before starting. Proceed only if you understand the risks. |
| **OEM Lock Delay** | Tecno devices often require you to **sign in to a Tecno account** and then wait up to **14 days** before the **"OEM unlocking"** option becomes available (it will be grayed out until then). Be patient! |

---

## 1. Preparation: On Your Tecno Phone

Before connecting your phone to the PC, you need to enable the hidden developer settings.

### 1.1 Enable Developer Options
* Go to **Settings** > **My Phone** (or **About Phone**).
* Tap repeatedly (**7 times**) on **Build Number** until you see the message: **"You are now a developer!"**

### 1.2 Enable Required Options
* Go to **Settings** > **System** > **Developer Options**.
* Toggle on **"OEM unlocking."** (Note if you have not signed up to Tecno account you need to do that and then wait 2 weeks Aka **14 days** before being able to enable this OEM unlocking option so take ur time)
* Toggle on **"USB debugging."** (Tap **Always Allow** checkbox and **Allow** button when connected to your pc after installing and running `adb devices`)

---

## 2. Preparation: On Your PC (Files and Tools)

Gather all the necessary tools and the device-specific files.

| File/Tool | Purpose | Link |
| :--- | :--- | :--- |
| **ADB & Fastboot** | Command line tools for communication. | [15-second ADB Installer (Recommended)](https://androidmtk.com/download-15-seconds-adb-installer) |
| **Stock Boot Image** | The original `boot.img` unique to your current firmware version. | Extract this from the official **KI5q** firmware file (e.g., from [NeedRom](https://www.needrom.com/download/tecno-spark-10-ki5q/)). |
| **Magisk APK** | The application used to patch the boot image and manage root access. | [Official Magisk GitHub Releases](https://github.com/topjohnwu/Magisk/releases) (**Get the latest stable version** only as of today it is Version 29.0) |

### 2.1 Install and Test ADB & Fastboot
1.  Run the **ADB Installer** on your PC. Press **Y** and **Enter** for all prompts, including the driver installation. In the Drivers step, it will pop up, just click **trust and install**.
2.  Open your **Terminal (Windows 11)** or **Command Prompt (CMD)**.
3.  Connect your phone to the PC via USB.
4.  Run the following command to check the connection:
    ```bash
    adb devices
    ```
5.  On your phone: You will see a prompt asking to **"Allow USB debugging."** Check the **"Always allow from this computer"** box and tap **"Allow."**
6.  Run `adb devices` again. You should see your device listed, followed by `device` (e.g., `099603739M001316 device`). **If so, we are good to go and proceed to next step.**

---

## 3. Unlock the Bootloader

**⚠️ Warning: This is the data-wiping step.**

1.  **Reboot to Bootloader Mode:**
    * In your CMD/Terminal, run:
        ```bash
        adb reboot bootloader
        ```
    * Your Tecno phone will reboot into **"Fastboot Mode."**

2.  **Execute the Unlock Command:**
    * Once in Fastboot Mode, run:
        ```bash
        fastboot flashing unlock
        ```

3.  **Confirm on Device (CRITICAL):**
    * Your phone screen will now display a final warning.
    * Use the **Volume buttons** to navigate.
    * Select the option to **"Unlock the Bootloader"** (or **"YES"**) and press the **Power button** to confirm.
    * *(Note: If you wish to not continue with this, **now is your last chance**. press **volume down** to go back, and press **volume up** to proceed with the unlocking)*

4.  **Wait for Wipe:** The device will perform a full factory reset and reboot.
    * **Crucial Setup Step:** Set up the phone again, but **skip all accounts and DO NOT set any screen lock** (PIN, pattern, or fingerprint, etc.). This prevents potential encryption issues later.

---

## 4. Patch the Boot Image with Magisk

We will use the Magisk app to modify your stock boot image, creating a "magisk-patched" file. You have to extract the `boot.img` from the firmware file you downloaded, it must **Match your build number and version** and extract that firmware, it usually comes in `.zip` you will find `boot.img`.

1.  **Transfer Files & Install Magisk:**
    * Copy the **Stock Boot Image** (`boot.img`) and **install the Magisk App** (Official Github page) onto your phone's internal storage.
    * Use a file manager to install the **Magisk App** on your phone (Press **Allow File manager to install applications** when prompted).

2.  **Patch the Image:**
    * Open the **Magisk app**.
    * Tap the **Install** button next to Magisk.
    * Choose **"Select and Patch a File."**
    * Navigate to and select the original **`boot.img`** file.
    * Tap **"Let's Go."** Magisk will process the file and save the output file, typically named **`magisk_patched-xxxx.img`**, in your **Downloads** folder.

3.  **Retrieve Patched File:**
    * Copy this new **`magisk_patched-xxxx.img`** file back to your PC (e.g., to `C:\adb`) using either:
        * **File Explorer:** Simply drag and drop the file via the Windows File Explorer on Windows.
        * **ADB Command:** (Recommended)
            ```bash
            adb pull /sdcard/Download/magisk_patched-xxxx.img .
            ```
            (Remember to replace the filename with the exact name Magisk generated.)

---

## 5. Flash the Patched Boot Image & Final Reboot

1.  **Reboot to Bootloader (Again):**
    * In your CMD/Terminal, run:
        ```bash
        adb reboot bootloader
        ```

2.  **Flash the Patched File:**
    * Run the `fastboot flash` command. **Crucial:** Replace `magisk_patched-xxxx.img` with the **exact and full name** of your patched file.
        ```bash
        fastboot flash boot magisk_patched-xxxx.img
        ```

3.  **Reboot to System:**
    * Once the flashing is complete and successful, run:
        ```bash
        fastboot reboot
        ```

Your phone should now boot up. Open the **Magisk app**, and it should confirm that your Tecno Spark 10 (KI5q) is **rooted!**
