# POS - Point Of Sales

# Table of Contents

- [1) Hardware](#1-hardware)
   - [1.1) Hardware Requirements](#11-hardware-requirements)
   - [1.2) Hardware Setup](#12-hardware-setup)
- [2) Software](#2-software)
   - [2.1) Client Build Environment Setup](#21-client-build-environment-setup)
   - [2.2) Database Server Setup](#22-api-keys)
   - [2.3) Running the Application](#23-running-the-application)

# 1) Hardware

## 1.1) Hardware Requirements

- [Any 96Boards CE](https://www.96boards.org/products/ce/) 3 Nos
- Compatible HDMI Monitor

## 1.2) Hardware Setup

- Make sure all the devices are connected on the same network

# 2) Software

**This guide assumes that [Debian OS is running on a Dragonboard410c](https://www.96boards.org/documentation/consumer/dragonboard410c/downloads/debian.md.html) on all 4 nodes. How ever the instructions hold true for other 96Boards CE Boards running Debian.**

> This project is compatible with other Linux based OS, but they might have to be tweaked accordingly.

## 2.1) Client Build Environment Setup

### Setup Zram Swap

Although the project itself doesn't consume much RAM, the NetBeans IDE can be
resource hungry so to be on the safe side, on boards with less than 1GB RAM its better to follow [this guide](https://www.96boards.org/documentation/consumer/guides/zram_swapspace.md.html)
to prevent random lock-ups.

### Install NetBeans
- Dependencies
  ```
  $ sudo apt update
  $ sudo apt dist-upgrade
  $ sudo apt install openjdk-10-jdk
  ```
- Download NetBeans: https://netbeans.org/downloads/
  - Make sure **Platform** is set to **Linux (x86/64)**
      > NOTE: Don't worry about the architecture, it will run natively on Arm.
- Download Java SE.
- Run the installer
  ```
  $ chmod +x netbeans-*.sh
  $ ./netbeans-*.sh
  ```
- When asked. set the JDK PATH as ```/usr/lib/jvm/java-10-openjdk-arm64```

## 2.2) Database Server Setup
- Install MariaDB/MySQL
  ```
  $ sudo apt install mysql-server
  ```
- Make server visible to other devices on the network
  ```
  $ sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
  ```
- Comment out the following line
  ```
  bind-address = 127.0.0.1
  ```
## 2.3) Running the Application

- **Set server IP Address**
  - In the files ```DatabaseInstaller.java``` and ```MainWindow.java``` edit the line ```host="jdbc:mysql://192.168.0.120:3306/"``` with the IP Address of your database server.
- **Initialize/Re-Initialize Database**
  - Run the ```DatabaseInstaller.java``` program and click on Initialize.
    > Note: If you want to re-initialize the whole database, select re-initialize.
- **Run the Application**
  - **Admin Node:** Login: admin, Password: tiger
  - **Employee/Kitchen Node:** Login: emp, Password: lion
  - **Customer Node:** Use the Signup page to create new customer IDs
