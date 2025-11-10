# 🚀 Tecno Spark 10 (KI5q) Ultimate Seamless Root Guide! 👑
*(Works with other Tecno models too!)*

This is your definitive, step-by-step guide to achieving **Ultimate Seamless Root** access on your **Tecno Spark 10 (KI5q)** using the **Fastboot method** and the powerful **Magisk** tool. We'll also cover the essential post-root steps to bypass security checks for your banking and sensitive apps.

***

## ⚠️ CRITICAL WARNINGS: READ BEFORE YOU START! 🚨

| Caution | Description | 🛑|
| :--- | :--- | :--- |
| **Data Wipe** | **Unlocking the bootloader will factory reset your device and erase ALL data.** 🗑️ Back up everything important (photos, contacts, app data, etc.) before proceeding. | 💾❌ |
| **Responsibility** | You proceed **at your own risk**. I am not responsible for any damage dealt to your device. Rooting and unlocking the bootloader will wipe all data. Ensure you understand the risks. | 💣🤯 |
| **OEM Lock Delay** | Tecno often forces a waiting period! You must **sign in to a Tecno account** and then wait up to **14 days** 🗓️ before the **"OEM unlocking"** option becomes available (it will be grayed out until then). Patience is key! | ⏳🔑 |

***

## 💻 Preparation: On Your Windows 10/11 PC

You must download and install the drivers from the provided links in **Section 2** before connecting your phone.

---

## 🐧 Preparation: On Your Linux PC (Tools & Drivers)

Linux users, you get the best experience! ADB and Fastboot are usually installed directly from your distribution's package manager, and special MTK drivers are often handled automatically by the kernel.

### 1. Install ADB and Fastboot (Best Terminal Guide)

Open your **Terminal** (`Ctrl+Alt+T`) and run the following commands. This guide assumes a Debian/Ubuntu-based distribution (`.deb` packages).

1.  **Update Package List:**
    ```bash
    sudo apt update
    ```
2.  **Install the Tools:**
    ```bash
    sudo apt install android-tools-adb android-tools-fastboot
    ```
    ✅ Done! The tools are now system-wide.

### 2. Setup USB Permissions (udev Rules)

To ensure you can communicate with your device without root privileges (`sudo`), you need to set up udev rules.

1.  **Add Your User to the `plugdev` Group:**
    ```bash
    sudo usermod -aG plugdev $USER
    ```
2.  **Install the Standard Android udev Rules (for seamless recognition):**
    ```bash
    sudo apt install android-sdk-platform-tools-core
    ```
3.  **Reboot for Changes to Take Effect:**
    ```bash
    reboot
    ```
> **💡 Linux Note on MTK Drivers:** You typically **do not** need separate MTK VCOM drivers. The Linux kernel has built-in support for MediaTek devices. The steps above are usually all you need.

***

## 📱 1. Preparation: On Your Tecno Phone

You need to enable the hidden developer settings before connecting the phone to the PC.

### 1.1 Enable Developer Options
* Go to **Settings** ⚙️ > **My Phone** (or **About Phone**).
* Tap repeatedly (**7 times** 👆) on **Build Number** until you see the message: **"You are now a developer!"**

### 1.2 Enable Required Options
* Go to **Settings** ⚙️ > **System** > **Developer Options**.
* Toggle on **"OEM unlocking."** (Remember the 14-day wait period! ⏳)
* Toggle on **"USB debugging."** (Check **Always Allow** and tap **Allow** when prompted after connecting and running `adb devices`).

***

## 🛠️ 2. Preparation: On Your PC (Files and Tools)

Gather all the necessary tools and the device-specific files.

| File/Tool | Purpose | Link |
| :--- | :--- | :--- |
| **ADB & Fastboot** (Windows Only) | Command line tools for communication. | [15-second ADB Installer (Recommended)](https://androidmtk.com/download-15-seconds-adb-installer) |
| **MTK VCOM Drivers** (Windows Only) | Special drivers for PC to recognize the Tecno phone. | [**Vcom MTK Drivers Signed**](https://mega.nz/file/3h8BSY5J#0sfvyru6Hl6FsryUO2v9Yi1mmtsE4wrze68L4rjSGNk) |
| **Stock Boot Image** | The original, unmodified kernel file for patching. Must **match your build number!** | Extract this from the official **KI5q** firmware file (e.g., from [NeedRom](https://www.needrom.com/download/tecno-spark-10-ki5q/)). |
| **Magisk App** | The tool used to patch the boot image and manage root access. | [Official Magisk GitHub](https://github.com/topjohnwu/Magisk/releases/latest) (**Get the latest stable version**, currently v29.0) |

> **📝 Crucial Note on Links:** The links for the **Drivers** and **Stock Firmware** do **NOT** belong to me. They are shared by third-party sources. **Download these files at your own risk** and always scan them with a security program before use. 🛡️

### 2.1 Install and Test ADB & Fastboot
**[How to install ADB & Fastboot on Windows 10/11 Youtube Guide](https://youtu.be/kLEPkRtYEY8)**
1.  **(Windows Only):** Run the **ADB Installer**. Press **Y** and **Enter** for all prompts, including the driver installation. Click **trust and install** in the pop-up.
2.  Open your **Terminal (Linux/Windows 11)** or **Command Prompt (CMD)**.
3.  Connect your phone to the PC via USB. 📱➡️💻
4.  Run the following command to check the connection:
    ```bash
    adb devices
    ```
5.  On your phone, accept the **"Allow USB debugging"** prompt. Check the **"Always allow..."** box and tap **"Allow."**
6.  Run `adb devices` again. You should see your device listed (e.g., `099603739M001316 device`). **If so, you are ready!** 👍

***

## 🔓 3. Unlock the Bootloader

**⚠️ Warning: This step will initiate the data wipe!** 

1.  **Reboot to Bootloader Mode:**
    * In your CMD/Terminal, run:
        ```bash
        adb reboot bootloader
        ```
    * Your Tecno phone will reboot into **"Fastboot Mode."** 🤖

2.  **Execute the Unlock Command:**
    * Once in Fastboot Mode, run:
        ```bash
        fastboot flashing unlock
        ```

3.  **Confirm on Device (CRITICAL):**
    * Your phone screen will show a final warning!
    * Use the **Volume UP** button to select **"Unlock the Bootloader"**.
    * *(Note: Press **Volume Down** to cancel if you change your mind—this is your last chance!)*

4.  **Wait for Wipe:** The device will perform a full factory reset and reboot. 🔄
    * **Crucial Setup Step:** Set up the phone again, but **SKIP ALL ACCOUNTS AND DO NOT SET A SCREEN LOCK** (PIN, pattern, etc.). This avoids encryption issues for now. (You can set your password/fingerprint later!)

***

## 🩹 4. Patch the Boot Image with Magisk

We will use the Magisk app installed on your phone to create a "magisk-patched" boot image. Remember, you must have the correct `boot.img` extracted from the firmware that **Matches your build number and version**.

1.  **Transfer Files & Install Magisk:**
    * **Transfer Stock Boot Image to Phone:**
    * Copy the **Stock Boot Image** (`boot.img`) from your PC to your phone's internal storage (e.g., to `/sdcard/Download`).

    * **Option A: File Explorer (Recommended for Beginners)** 📂
        * Connect your phone to the PC and ensure it's set to **File Transfer** mode.
        * Open Windows File Explorer, navigate to your phone's internal storage, and drag the `boot.img` file into the `Download` folder.

    * **Option B: ADB Command** (More reliable for long paths) 💻
        * Open your CMD/Terminal on your PC and run:
            ```bash
            adb push "C:\path\to\your\boot.img" /sdcard/Download/boot.img
            ```
            *(Remember to replace `"C:\path\to\your\boot.img"` with the actual location of the file on your PC.)*
    * Install the **Magisk App** (`.apk` file) on your phone. (Allow file manager to install applications when prompted).

2.  **Patch the Image:**
    * Open the **Magisk app** 🦊.
    * Tap the **Install** button next to Magisk.
    * Choose **"Select and Patch a File."** 
    * Navigate to and select the Stock **`boot.img`** file from your phone's storage.
    * Tap **"Let's Go."** Magisk will save the output file, typically named **`magisk_patched-xxxx.img`**, in your **Downloads** folder.

3.  **Retrieve Patched File (Example using ADB):**
    * Copy this new **`magisk_patched-xxxx.img`** file back to your PC (e.g., to your `C:\adb` folder or your home directory).
    * In your CMD/Terminal, run:
        ```bash
        adb pull /sdcard/Download/magisk_patched-xxxx.img .
        ```
        *(Remember to replace `magisk_patched-xxxx.img` with the exact filename Magisk generated.)*

***

## ⚡ 5. Flash the Patched Boot Image & Final Reboot

1.  **Reboot to Bootloader (Again):**
    * In your CMD/Terminal, run:
        ```bash
        adb reboot bootloader
        ```

2.  **Flash the Patched File:**
    * Run the `fastboot flash` command. **Crucial:** Replace the placeholder filename with the **exact and full name** of your patched file.
        ```bash
        fastboot flash boot magisk_patched-xxxx.img
        ```

3.  **Reboot to System:**
    * Once the flashing is complete and successful:
        ```bash
        fastboot reboot
        ```

Your phone should now boot up normally. Open the **Magisk app**, and it should happily confirm that your Tecno Spark 10 (KI5q) is **ROOTED!** 🎉

***

## 🛡️ 6. Post-Root: Hiding Root (SafetyNet/Bank Apps)

To make banking and secure apps work, you must hide Magisk from Google's security checks (SafetyNet / Play Integrity API).

### 6.1 Enable Zygisk:
1.  Open the **Magisk App**.
2.  Go to **Settings** ⚙️.
3.  Toggle on **Zygisk** (if not enabled by default).
4.  **Reboot** your phone. 🔄

### 6.2 Configure DenyList (Hide Root from Apps):
1.  Go back to Magisk **Settings**.
2.  Tap on **Configure DenyList**. 
3.  Tap the **three-dot menu** ⋮ in the top corner and select **"Show system apps"**.
4.  Scroll through and find all sensitive apps (banking, payment apps, Google Play Services, Google Play Store, etc.).
5.  **Crucial:** Tap to check the box next to **every component** of the sensitive app—don't just check the main app name; expand the list and check all sub-processes/components! ✅

### 6.3 Check Status:
1.  After setting the DenyList and rebooting, your banking apps should now launch and function normally! Enjoy your **seamlessly rooted** device! 🥳
