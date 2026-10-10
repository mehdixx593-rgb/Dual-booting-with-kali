🐉 Before You Dual Boot Kali Linux: 9 Things to Check

Planning to install Kali Linux alongside Windows? Read this first.

Dual booting lets you run two operating systems on the same computer. However, mistakes during partitioning or boot configuration can cause data loss or prevent an operating system from starting.

This guide covers the essential checks to perform before installing Kali Linux alongside Windows, particularly on modern UEFI-based laptops.

📋 Table of Contents

1. "Back Up Your Data" (#1-back-up-your-data)
2. "Check Your Boot Mode" (#2-check-your-boot-mode)
3. "Check Your Disk Partition Style" (#3-check-your-disk-partition-style)
4. "Check Available Disk Space" (#4-check-available-disk-space)
5. "Check BitLocker and Device Encryption" (#5-check-bitlocker-and-device-encryption)
6. "Understand Fast Startup and Hibernation" (#6-understand-fast-startup-and-hibernation)
7. "Check Secure Boot" (#7-check-secure-boot)
8. "Check Hardware Compatibility" (#8-check-hardware-compatibility)
9. "Prepare Your Kali USB" (#9-prepare-your-kali-usb)
10. "Final Checklist" (#-final-checklist)

---

1. 💾 Back Up Your Data

Never start partitioning without a backup.

A mistake during installation can erase the wrong partition or damage your existing Windows installation.

Before proceeding:

- Back up important documents, photos, projects, and other files.
- Use an external drive or trusted cloud storage.
- Verify that your backup files can actually be opened.
- Save your Windows recovery key if device encryption is enabled.

Remember: a backup you have never tested is only a backup in theory.

2. 🖥️ Check Your Boot Mode

Your computer may use UEFI or Legacy BIOS boot mode.

How to check

1. Press "Win + R".
2. Type "msinfo32".
3. Press Enter.
4. Find BIOS Mode in System Information.

You should see either "UEFI" or "Legacy".

Modern Windows 11 installations generally use UEFI.

Why it matters: Windows and Kali should normally be installed and configured to boot in compatible modes. For a typical modern system, use UEFI rather than switching an existing Windows installation to Legacy mode.

3. 💽 Check Your Disk Partition Style

Windows disks commonly use one of two partitioning schemes:

- GPT: The modern standard, normally used with UEFI.
- MBR: An older partitioning scheme commonly associated with Legacy BIOS.

How to check

1. Press "Win + X".
2. Open Disk Management.
3. Right-click the disk containing Windows.
4. Select Properties.
5. Open the Volumes tab.
6. Find Partition style.

For a typical UEFI-based Windows installation, GPT is expected.

Important: Check the correct physical disk. If your laptop has multiple drives, do not assume they all use the same partition style.

4. 📦 Check Available Disk Space

Kali needs space for the operating system, tools, updates, and your own files.

As a practical guideline:

- 25 GB: A tight starting point for a basic installation.
- 50 GB or more: A more comfortable starting point.
- 100 GB or more: Worth considering for extensive tools, development, and cybersecurity labs.

Actual requirements depend on what you install and how you use Kali.

How to create unallocated space

1. Press "Win + X".
2. Open Disk Management.
3. Right-click your Windows "C:" partition.
4. Select Shrink Volume.
5. Enter the amount of space to shrink.
6. Confirm the operation.

Windows should create a region labeled Unallocated.

Leave this space unallocated for the Kali installation.

Do not delete unfamiliar partitions or format the unallocated space as a new Windows volume. The Kali installer can use the space you prepared.

5. 🔐 Check BitLocker and Device Encryption

Windows 11 laptops may have BitLocker or Device Encryption enabled.

Changes to firmware settings or the boot environment can trigger a BitLocker recovery prompt.

Before proceeding:

1. Check whether BitLocker or Device Encryption is enabled.
2. Locate and securely save your recovery key.
3. Verify that you can access the key from another device if necessary.
4. Follow the appropriate guidance for suspending protection if your installation procedure requires it.

To check BitLocker status, open an administrator terminal and run:

manage-bde -status

Important: Suspending BitLocker protection is not the same as decrypting the drive. Do not permanently disable encryption without a specific reason.

Official guidance: https://support.microsoft.com/windows/find-your-bitlocker-recovery-key

6. ⚡ Understand Fast Startup and Hibernation

Windows Fast Startup uses hibernation technology to speed up startup.

A hibernated Windows session can leave an NTFS filesystem in a state that makes writing to it from Linux unsafe.

How to disable Fast Startup

1. Open Control Panel.
2. Select Power Options.
3. Choose Choose what the power buttons do.
4. Select Change settings that are currently unavailable, if shown.
5. Uncheck Turn on fast startup, if available.
6. Save your changes.

You can also disable hibernation using an administrator Command Prompt:

powercfg /h off

This disables hibernation, including the functionality used by Fast Startup.

Important: Disabling Fast Startup is a precaution, not a substitute for shutting Windows down properly. Never force writes to a Windows partition that is hibernated or otherwise in an unsafe state.

7. 🛡️ Check Secure Boot

Secure Boot is a UEFI security feature that helps prevent unauthorized boot components from loading.

Do not automatically disable it before installing Kali.

First, try booting the official Kali installer with your current firmware settings. If it fails, consult the current Kali documentation to determine whether Secure Boot is responsible.

If a firmware change is necessary, many HP laptops provide access to startup options through "Esc" and BIOS Setup through "F10".

Security note: Disabling Secure Boot reduces boot-time protection. Change it only when necessary, and understand how to restore it afterward.

8. 📡 Check Hardware Compatibility

Some hardware may require additional firmware, drivers, or configuration under Linux.

Check the following:

Wi-Fi adapter

Intel adapters are often straightforward to use, but compatibility depends on the exact model. Some Realtek and Broadcom adapters may require additional setup.

Identify your wireless adapter model and check its Linux support before installation.

NVIDIA graphics

Some NVIDIA GPUs require additional driver configuration. The exact requirements depend on the GPU and driver version.

You generally do not need to configure GPU drivers before installing Kali.

Other hardware

Check whether your essential components work:

- Wi-Fi and Ethernet.
- Keyboard and touchpad.
- Audio.
- Bluetooth.
- Screen brightness.
- Suspend and resume.

Where possible, boot the Kali live environment and test your hardware before installing the operating system.

9. 🔌 Prepare Your Kali USB

Download the official ISO

Download Kali Linux from:

https://www.kali.org/get-kali/

Avoid unofficial downloads.

Verify the checksum

Verifying the SHA-256 checksum helps confirm that the downloaded ISO matches the published checksum.

On Windows, open PowerShell and run:

Get-FileHash .\kali-linux-installer-amd64.iso -Algorithm SHA256

Replace the filename with the name of your downloaded ISO.

Compare the resulting hash with the checksum published by Kali for that exact image.

Official downloads and verification guidance:

https://www.kali.org/docs/introduction/download-official-kali-linux-images/

Create a bootable USB

Common tools include:

- Rufus: https://rufus.ie/
- balenaEtcher: https://etcher.balena.io/

An 8 GB or larger USB drive is a practical starting point, depending on the image.

For a typical modern laptop, select settings compatible with UEFI and the image you downloaded. Follow the tool's instructions rather than assuming every ISO requires identical settings.

Warning: Creating a bootable USB usually erases the USB drive's existing contents. Back up those files first.

Know your HP boot menu key

Common HP startup keys include:

Key| Function
"Esc"| Opens the Startup Menu on many models
"F9"| Opens Boot Device Options on many models
"F10"| Opens BIOS Setup on many models

Exact behavior varies by model.

When starting the laptop, open the boot menu and select the USB's UEFI boot entry when appropriate.

---

✅ Final Checklist

Before installing Kali, confirm that:

- [ ] Important files are backed up and verified.
- [ ] The current boot mode is known.
- [ ] The Windows disk's partition style is known.
- [ ] Enough disk space is available.
- [ ] Unallocated space has been prepared if needed.
- [ ] BitLocker or Device Encryption status has been checked.
- [ ] The recovery key is safely accessible.
- [ ] Fast Startup and hibernation have been addressed.
- [ ] Secure Boot compatibility has been considered.
- [ ] Essential hardware compatibility has been checked.
- [ ] The official Kali ISO has been downloaded and verified.
- [ ] The bootable USB has been created.
- [ ] The laptop's boot menu key is known.

Final Advice

The most dangerous part of dual booting is not launching Kali. It is selecting the correct disk and partitions during installation.

When you reach the installer, carefully identify the target disk and the unallocated space you prepared.

Do not format or delete Windows, EFI System, or recovery partitions unless you fully understand why the operation is necessary.

If you are unsure what a partition does, stop and investigate before continuing.

A successful dual boot means having Kali available without unnecessarily sacrificing your Windows installation or personal data.

---

Disclaimer

This guide covers a typical Windows and UEFI dual-boot setup. Exact requirements and procedures vary by laptop, firmware, Windows configuration, and Kali release. Consult the official documentation before making partitioning or firmware changes.
