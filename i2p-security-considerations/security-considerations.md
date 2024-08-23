# Security Consideration's

Utilizing a remote server for I2P operation carries inherent risks associated with online servers. As the server is connected to the internet, it becomes a potential target for hackers and other malicious entities seeking to exploit vulnerabilities or gain unauthorized access. Thus, server security is a critical aspect of maintaining the integrity and confidentiality of your I2P network. This includes implementing strong access controls, ensuring software and system updates are timely installed, employing intrusion detection and prevention systems, and routinely monitoring the server for any suspicious activities.

#### Change Default SSH Port <a href="#change-default-ssh-port" id="change-default-ssh-port"></a>

Changing the default SSH port enhances security by reducing the likelihood of automated attacks. Many bots and malicious scripts target the default port (22), so changing it to a non-standard, high-numbered port can help avoid basic port scan attacks, acting as a simple but effective layer of security.

```
sudo vim -c "%s/#Port 22/Port 2222/g | wq" /etc/ssh/sshd_config && sudo systemctl restart sshd
```

The command above will change the default port from **22** to **2222.** If you want to change to another port just update the command above. You can select any port from 1-65536 providing it is not in use.

#### Enabling Firewall <a href="#enabling-firewall" id="enabling-firewall"></a>

Firewalls are essential as they act as a protective barrier between your internal network (or individual computer) and external threats on the internet. They monitor and control incoming and outgoing network traffic based on predetermined security rules, blocking malicious traffic, and preventing unauthorized access and cyberattacks. Without a firewall, your system is exposed and vulnerable to these threats, jeopardizing the safety of your data and overall network.

1. First we need to install a firewall, the easiest firewall we found is **UFW**.

```
apt update && apt upgrade -y && apt install ufw
```

1. Next we need to enable some ports.
   1. SSH
   2. I2P Remote Console
   3. I2P HTTP Proxy
   4. I2P UDP Port

```
ufw default allow outgoing
ufw default allow incoming
ufw allow 2222
ufw allow 7777
ufw --force enable
```

**ufw default allow outgoing -** This changes the default firewall policy to allow all outgoing traffic by default.

**ufw default allow incoming -** This changes the default firewall policy to deny all incoming traffic by default.

**ufw allow 2222 -** This rule opens the ssh port, you will need to update this number if you selected a different ssh port above.

**ufw allow 7777 -** The rule opens the I2P port, this port number will be different for every user. To find your I2P port ensure you are connected to the I2P router ([Instruction's](https://docs.stormycloud.org/i2p-guides/how-to-create-ssh-tunnel)) and visit the [I2P Router Console Network Page](http://127.0.0.1:7657/confignet). The I2P Ports are selected automatically please update the command above with the correct port for your configuration. The ports required will be towards the bottom of the page.

**ufw --force enable -** This command enables the UFW firewall.
