# Setting up Linux I2P+ Node

This guide provides step-by-step instructions for installing and configuring an I2P node on Debian-based systems. Although the commands mentioned here are specific to Debian, most Linux distributions support I2P.

**Requirements:**

* Memory: By default, I2P only requires 128MB of memory. However, we recommend a minimum of 1GB and suggest 2GB for optimal performance.
* CPU: I2P has been tested and works on a wide range of systems, from single-board CPUs to enterprise-grade CPUs. The minimum requirement is 1 core, but we recommend at least 2 cores for better performance.
* For optimal performance and to effectively assist the I2P network, it is recommended to have a 24/7 internet connection.

**Step 1** - To ensure a smooth installation process, it is important to fetch the necessary prerequisites and update your server.

```
sudo apt update && sudo apt upgrade -y && sudo apt install default-jdk wget -y    
```

<figure><img src="../.gitbook/assets/image (5).png" alt="" width="523"><figcaption></figcaption></figure>

**Step 2 -** To maintain optimal security and system integrity, it is not recommended to run I2P as a root user. Therefore, we will be initiating a new user profile specifically to operate the I2P-router.

```
sudo adduser i2p && sudo usermod -aG sudo i2p
```

<figure><img src="../.gitbook/assets/image (6).png" alt="" width="523"><figcaption></figcaption></figure>

**Step 3 -** Moving forward, let's transition to the recently created user profile and proceed with retrieving the necessary I2P software components.

```
Note: At the time of writing this, 2.6.0 was the latest release, so our URLs in the examples reflect that. To check for the latest releases, view and amend the instructions as needed below.
https://i2pplus.github.io/
```

```
su i2p
cd ~/
wget http://i2pplus.github.io/installers/i2pinstall_2.6.0+.exe
```

<figure><img src="../.gitbook/assets/image (7).png" alt="" width="523"><figcaption></figcaption></figure>

**Step 4 -** After download, execute the headless Java installer for a quick, terminal-based setup. If your language of choice is english you can leave all settings as default.

```bash
java -jar i2pinstall_2.6.0+.exe -console
```

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

**Step 5 -** It's crucial to ensure that I2P initiates automatically upon server reboot, guaranteeing continuous functionality.

```
sudo echo '/bin/su i2p -c "/home/i2p/i2p/i2prouter start"' | sudo tee -a /etc/rc.local && sudo chmod +x /etc/rc.local
```

<figure><img src="../.gitbook/assets/image (9).png" alt="" width="523"><figcaption></figcaption></figure>

**Step 6 -** We need to start I2P.

```
./i2prouter start
```

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

The next step will depend on your system configuration. If you have a desktop environment installation please skip to Post Installation Instructions. If your server is remote please skip to [How to create SSH Tunnel](https://docs.stormycloud.org/i2p-guides/how-to-create-ssh-tunnel).

**Step 7 -** Congratulations you have successfully configured an I2P node. New nodes can take some time to integrate with the network. So not all I2P websites & application will work straight away and can take some time for the router to be intergrated into the I2P Network. Learn more about [accessing the I2P Network & Applications.](accessing-i2p-network-and-applications.md)

