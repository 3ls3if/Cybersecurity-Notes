# 🧑‍💼 Insider Attack

## Tools & Preparation

* You should arrive prepared with everything you need to conduct your attack since you may not have an opportunity to download anything from the outside once you’re in.
* Have all the tools you are likely to need with you on removable media such as a USB drive or CD.
*   In the most difficult cases, such as a fully locked CMOS

    and full disk encryption, you may even want to bring a hard drive with a prepared operating system on it so that you can attempt to gain access to the subject network from

    the provided equipment.

## Orientation

The most common configuration you’ll encounter is the Windows workstation, a stand- alone PC or laptop computer running a version of Microsoft Windows. It will most likely be connected to a wired LAN and utilize the Windows domain login. You’ll be given a domain account. Log in and have a look around. Take some time to “browse” the network using the Windows file explorer. You may see several Windows domains as well as drives mapped to file servers, some of which you may already be connected to. The whole point of the insider attack is to find sensitive information, so keep your eyes open for servers with descriptive names such as “HR” or “Engineering.” Once you feel comfortable that you know the bounds of your account and have a general view of the network, it’s time to start elevating your privilege level.

## Gaining Local Admin Privileges

```
# View users under local admins group
net localgroup Administrators
```

### Reset Admin Password Using Offline NT Password and Registry Editor

```
### Boot from the Media:

1. Insert the bootable USB drive or CD/DVD into the target computer.
2. Restart the computer and enter the BIOS/UEFI settings (usually by pressing F2, F12, DEL, or ESC during startup).
3. Change the boot order to boot from the USB drive or CD/DVD.

### Run the Tool:

1. The Offline NT Password & Registry Editor will boot into a text-based interface.
2. Follow the on-screen prompts:
   - **Select the Partition**: Choose the partition where Windows is installed (usually the default is correct).
   - **Select the Password Reset Option**: Choose “Password Reset” to modify user accounts.

### Edit User Accounts:

1. **List Users**: The tool will display a list of user accounts. Identify the account for which you want to reset the password.
2. **Edit User**: Select the account and choose the appropriate option:
   - **Clear the Password**: This option removes the password entirely, allowing you to log in without a password.
   - **Set a New Password**: You can set a new password if desired.

### Save Changes:

1. After making changes, the tool will prompt you to save the modifications. Confirm the changes to write them to the disk.

### Reboot the Computer:

1. Remove the bootable media from the computer.
2. Restart the system. You should now be able to log in without the old password or with the new one if you set it.

```

### Copy SAM File to a USB

```
<Invoke pseudo terminal using ALT-F2>

# Mount the usb drive
mount /dev/sdb1 /mnt

# Copy the SAM and SECURITY file into the usb
cp /drive/WINDOWS/system32/config/SAM /mnt
cp /drive/WINDOW/system32/config/SECURITY /mnt

<Return to the menu using ALT-F1 and press ENTER>
```

## Recovering Admins Password

* Bringing rainbow tables and software with you on a large USB hard drive&#x20;
* Using a dictionary attack with Cain or L0phtCrack&#x20;
* Taking the SAM file back to your office to crack overnight&#x20;
* Sending the SAM file to a member of your team on the outside
