# Guide: Remote Linux Installation via Nighthawk WiFi

This guide explains how to set up a "viewer" and prepare for installing Linux on other computers in your home network.

## 1. Prepare the Installation Media (Bootable USB)

To install Linux, you first need a bootable USB drive.

- **Recommended Tool:** [Ventoy](https://www.ventoy.net/) or [BalenaEtcher](https://www.balena.io/etcher/).
- **Linux ISO:** Download an ISO like Ubuntu, Fedora, or Linux Mint.
- **Steps:**
  1. Plug in your USB drive.
  2. Use Etcher to "Flash" the ISO to the USB.

## 2. The "Viewer" (Remote Desktop)

Since you want to see the screen of the other computer from your current one:

### Option A: RustDesk (Easiest)

RustDesk is an open-source remote desktop software that works like TeamViewer but is free and great for local networks.

#### How to Install RustDesk

1. Go to [RustDesk.com](https://rustdesk.com/) on both your main and target computers.
2. Download the installer for your operating system (Windows, Linux, or macOS).
3. Run the installer and follow the on-screen instructions to complete the installation.
4. Open RustDesk after installation.

#### How to Use RustDesk for Remote Access

- On the **target computer**, open RustDesk and note the displayed ID and password.
- On your **main computer**, open RustDesk, enter the target computer's ID, and click Connect.
- Enter the password when prompted to gain remote access.

You can now control the target computer remotely to start the Linux installation process.

### Option B: VNC (During Installation)

Some Linux installers (like Fedora or Ubuntu Server) allow you to enable a VNC server during the setup.

- You would use a **VNC Viewer** (like [RealVNC](https://www.realvnc.com/en/connect/download/viewer/)) on your main computer.

## 3. Nighthawk WiFi Configuration

To ensure the computers can see each other:

1. Connect both computers to your **Nighthawk** WiFi.
2. Ensure "Guest Network" is **OFF** (Guest networks often block devices from talking to each other).
3. Note the IP address of the target computer.

## 4. Remote Installation Steps

1. **Boot the target computer** from the USB.
2. **Connect to WiFi** immediately in the "Live" environment.
3. **Enable Remote Desktop** in the Live environment (Settings -> Sharing -> Remote Desktop in Ubuntu).
4. **Open the Viewer** on your main computer and connect using the target's IP address.
5. **Start the Installer** from within the remote session.

---

_Note: If the target computer has no OS at all, you will need to physically be at the machine to start the USB boot and connect it to WiFi before the "Viewer" can take over._
