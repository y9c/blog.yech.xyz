+++
title = "Connect Campus Vpn in WSL Command Line"
description = ""
featured_image = "/img/Cisco-AnyConnect-Logo.png"
date = 2022-10-30T23:27:47-05:00
categories = ["geek"]
tags = ["linux", "VPN"]
comment = true
+++

WSL (Windows Subsystem for Linux) is becoming more and more powerful and stable these days, but the internet connection is still not easy to use.
When you connect VPN in the host machine, the networking will lost, or the DNS won't resolve by default.

- https://github.com/microsoft/WSL/issues/1350
- https://github.com/microsoft/WSL/issues/5068

This is because WSL is not in the sample network as the host machine.
If we can start VPN client in WSL directly, all the problem will not happen.

Most university use Cisco Anyconnect for the VPN connection. `openconnect` is the open source version of this tool, and it works in Linux system.
More importantly, the command line mode in supported.

This is very straightforward until recent years.
For security isssue, most school enforce 2FA for VPN login, and you have to enter your username and password through a popup webpage. This is called SSO (Single Sign-On).
But the `openconnect` tool do not support this.
Fortunately, someone has modified this to support sso, and the code is also open source (https://github.com/vlaci/openconnect-sso).

The manual shows that you can install `openconnect-sso` by two line of codes:

```bash
pip install --user pipx
pipx install "openconnect-sso"
```

But, some modification are required to make it work under WSL.

- Firstly, install the the qt5 library.

```bash
# for Archlinux
pacman -S qt5
# for ubuntu
apt install qt5-default
```

- Seconcdly, you need to install `pyqt5` and `PyQtWebEngine` python package. This is very tricky, because pipx do not use the python under your PATH, but the one under its virtual environment.
  Thus, you need to install `pyqt5` and `PyQtWebEngine` for python under virtual environment.

```bash
~/.local/pipx/venvs/openconnect-sso/bin/python -m pip install pyqt5 PyQtWebEngine
```

- note: You can check the path of the python by `head -1 $(which openconnect-sso)` command.

Running this tool is also tricky.

- Firstly, you might need to modify the `QTWEBENGINE_CHROMIUM_FLAGS` variable for some Linux system, or the popup page will be blank.

```bash
export QTWEBENGINE_CHROMIUM_FLAGS="--no-sandbox"
```

- Secondly, you should NOT specific the user name in the command line, or the webpage will keep freshing.

```bash
openconnect-sso --server vpn.yourschoolname.edu
```
