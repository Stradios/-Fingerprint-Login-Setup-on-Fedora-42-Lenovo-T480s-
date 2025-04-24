# 🛡️ Fingerprint Login Setup on Fedora 42 (Lenovo T480s)

This guide explains how to enable fingerprint login and sudo authentication on **Fedora 42** with a **Lenovo ThinkPad T480s** using the **Synaptics Metallica MIS Touch Fingerprint Reader** (`06cb:009a`).

---

## 📋 Prerequisites

Make sure your fingerprint sensor is recognized:

```bash
lsusb
```

Look for something like:

```
Bus 001 Device 012: ID 06cb:009a Synaptics, Inc. Metallica MIS Touch Fingerprint Reader
```

---

## 📦 1. Install Required Packages

Install the necessary software via DNF:

```bash
sudo dnf install fprintd python-validity open-fprintd
```

---

## ⚙️ 2. Enable the Fingerprint Service

Start and enable the `python-validity` service:

```bash
sudo systemctl enable --now python3-validity
```

---

## 🧪 3. Verify Fingerprint Reader

Check if the fingerprint device is working:

```bash
fprintd-list $USER
```

If it's detected, you can proceed with enrollment.

---

## 👆 4. Enroll a Fingerprint

Start the fingerprint enrollment process:

```bash
fprintd-enroll
```

Follow the prompts to scan your finger several times.

---

## 🔐 5. Enable Fingerprint for Login and Sudo

Enable fingerprint authentication with:

```bash
sudo authselect enable-feature with-fingerprint
```

Alternatively, go to:

```
Settings → Users → Fingerprint Login → Add Fingerprint
```

---

## 🧼 Optional Fix: Reset Fingerprint Data

If enrollment fails, try resetting:

```bash
sudo rm -r /var/lib/fprint/*
sudo systemctl restart python3-validity
```

Then repeat the enrollment step.

---

## ✅ 6. Test Authentication

- Lock your session and try logging in with your finger
- Run a `sudo` command and scan your finger when prompted

---

## 🧠 Notes

- Works on **Fedora 42**
- Tested on **Lenovo ThinkPad T480s** with `06cb:009a` fingerprint reader
- Desktop: **GNOME**, but should work on others with PAM support

---

Feel free to fork, clone, or adapt this guide for your own setups. Issues and suggestions are welcome!
