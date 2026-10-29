# Cybersecurity Testing Lab (VirtualBox + Kali Linux)

This document explains each step of the lab setup, based on the screenshots taken during the build.

## Lab Overview

| Item | Value |
|------|-------|
| Hypervisor | VirtualBox 7.2.22 + Extension Pack |
| Attacker VM | Kali Linux |
| Network | NAT Network `NatNetwork`, subnet `10.0.0.0/24` |
| Kali IP | `10.0.0.2/24` |
| Clipboard | Bidirectional |
| Drag and Drop | Bidirectional |
| Shared folder | Host `Downloads` folder |
| Internet | Full access |

---

## Step 1: Download VirtualBox and the Extension Pack (Screenshot 1)

The screenshot shows the official VirtualBox download page for version **7.2.22**, the latest release used in this lab.

- On the left, **Platform Packages** lists installers per host OS (Windows, macOS Intel, macOS Apple Silicon, Linux, Solaris). The Windows host package was used for the base installation.
- On the right, the **Extension Pack** (same version, 7.2.22) is downloaded through "Accept and download" after reading the PUEL license. The Extension Pack adds features such as USB 2.0/3.0 support and is installed on top of the base package. Its version must match the VirtualBox version.

## Step 2: VirtualBox Manager (Screenshot 2)

This is the VirtualBox Manager home screen after installation. The left sidebar gives access to Machines, Extensions, Media, **Network** (used in the next step), Cloud and Resources. The toolbar provides New, Open, Preferences, Import and Export.

## Step 3: Create the NAT Network (Screenshot 3)

Under **Network > NAT Networks**, a network named **`NatNetwork`** was configured with the IPv4 prefix **`10.0.0.0/24`**, which gives the lab its required subnet.

What the fields mean:
- **Name:** the label the VM selects in its network settings.
- **IPv4 Prefix:** the address range of the lab network. `10.0.0.0/24` covers `10.0.0.1` to `10.0.0.254`. The `.1` address is used by VirtualBox as the gateway.
- **Enable DHCP:** automatic address assignment. It is left off for this lab because Kali uses a fixed address.
- **Enable IPv6:** not needed, so it stays off.

The change only takes effect after **Apply**, and the table at the top then shows `10.0.0.0/24` for `NatNetwork`.

A NAT Network lets all VMs on it talk to each other and reach the internet, while hiding them behind the host.

## Step 4: Download Kali Linux (Screenshot 4)

The screenshot shows the Kali download page with the **Installer** image marked as Recommended (about 4.7 GB). It is a complete offline installer with customization options, and it is used to install Kali into a new VirtualBox VM.

## Step 5: Enable Drag and Drop (Screenshot 5)

In the VM settings (Expert mode, **General > Features**), **Drag-and-Drop** is set to **Bidirectional**. This allows files to be dragged from the host into Kali and from Kali back to the host. The setting works together with VirtualBox Guest Additions inside the VM.

## Step 6: Enable Shared Clipboard (Screenshot 6)

In the same section, **Shared Clipboard** is set to **Bidirectional**. Text copied on the host can be pasted in Kali and the other way round.

## Step 7: Attach the VM to the NAT Network (Screenshot 7)

In the VM's **Network** settings, **Adapter 1** is configured as follows:

- **Enable Network Adapter:** checked
- **Attached to:** NAT Network
- **Name:** `NatNetwork` (the network created in Step 3)
- **Adapter Type:** Intel PRO/1000 MT Desktop (82540EM)
- **Promiscuous Mode:** Allow All. This lets the VM see all traffic on the virtual network, which is useful for sniffing and scanning tools.
- **Virtual Cable Connected:** checked, so the adapter behaves as if plugged in.

## Step 8: Shared Folder (Screenshot 8)

Under **Shared Folders**, a machine folder was added:

- **Name:** `Downloads`
- **Path:** `C:\Users\null\Downloads` (the host's Downloads folder)
- **Access:** Full (read and write)

Auto-mount and Make Permanent should be enabled so the folder appears automatically in Kali after every boot. The user must also belong to the `vboxsf` group in Kali to access it.

## Step 9: Internet Test (Screenshot 9)

The Kali terminal shows `ping google.com` succeeding:

- Name resolution worked (google.com resolved to `192.178.204.100`), so DNS is functioning.
- 3 packets sent, 3 received, **0% packet loss**, average round trip about 82 ms.

This confirms Kali has working internet access through the NAT Network.

---

## Remaining Evidence to Add

- Screenshot of Kali's network settings or terminal showing the static address **`10.0.0.2/24`** and gateway `10.0.0.1` (the ping screenshot proves internet but not the address).
- Screenshot of the shared `downloads` folder opened inside Kali.
- Screenshot showing the VirtualBox "Invalid settings detected" warning cleared.

## Notes

- The host cannot reach VMs on a NAT Network directly unless port forwarding is configured.
- Additional targets (for example Metasploitable) can join the same network with other addresses in `10.0.0.0/24`.
- Use this lab only on systems you own or are authorized to test.



<img width="1568" height="764" alt="preview (9)" src="https://github.com/user-attachments/assets/de37c23e-1a74-4650-a3c8-1063c9faf071" />


<img width="560" height="479" alt="preview" src="https://github.com/user-attachments/assets/cb300cc9-c2c9-4a61-a3a0-a4838e30f378" />



<img width="1273" height="516" alt="preview (1)" src="https://github.com/user-attachments/assets/7c3a53f7-e534-455f-97a9-c4068cdbc4e9" />


<img width="1568" height="779" alt="preview (2)" src="https://github.com/user-attachments/assets/2994967a-8da0-4353-936e-342921fad01c" />


<img width="974" height="525" alt="preview (3)" src="https://github.com/user-attachments/assets/7df5f911-2cae-46fd-94e6-b14573e2b9c4" />


<img width="969" height="550" alt="preview (4)" src="https://github.com/user-attachments/assets/06cafd57-eca5-47c0-ad03-59a1c1b5aac5" />


<img width="980" height="639" alt="preview (5)" src="https://github.com/user-attachments/assets/2549a496-b141-4674-a8e1-1752c1cbdffa" />


<img width="974" height="635" alt="preview (6)" src="https://github.com/user-attachments/assets/681c4092-b736-4b18-a8fc-a781ebe69649" />


<img width="647" height="363" alt="preview (7)" src="https://github.com/user-attachments/assets/895bcb5c-a672-4188-a84c-b225e03bcbff" />


