# Updating I2P Outproxy

## I2P/I2P+

As of [August 2022 ](https://geti2p.net/en/blog/post/2022/08/04/Enable-StormyCloud)the I2P team made StormyCloud the default outproxy provider for I2P. The default outproxy provider for I2P+ is purokishi.i2p. However, if you need to update the outproxy information please follow the below steps. If you are connecting to a remote server you will want to follow our [SSH Tunnel guide](how-to-create-ssh-tunnel.md).

1.  Connect to your router console - [127.0.0.1:7657](http://127.0.0.1:7657/home)\


    <figure><img src="../.gitbook/assets/image (30).png" alt="" width="563"><figcaption></figcaption></figure>
2. Navigate to the [Tunnel Manager.](http://127.0.0.1:7657/tunnelmanager)

<figure><img src="../.gitbook/assets/image (32).png" alt="" width="563"><figcaption></figcaption></figure>

3. Click on the [I2P HTTP Proxy](http://127.0.0.1:7657/i2ptunnel/edit?tunnel=0).
4. Update both the Outproxies and SSL Outproxies to **exit.stormycloud.i2p** and hit the Save button.

<figure><img src="../.gitbook/assets/image (33).png" alt="" width="563"><figcaption></figcaption></figure>

## I2PD

To add an Outproxy for I2PD, you will need to update the i2pd.conf file. You can either use our simple one-line command to do this automatically or follow the instructions below.

```
curl -sSL https://stormycloud.org/scripts/i2pd.sh | bash
```

1. We need to open the i2pd configuration file, we can do this in nano or vim.

```
nano /etc/i2pd/i2pd.conf
```

2. Locate the block starting with \[httpproxy].
   1. Add in the following line **outproxy = http://exit.stormycloud.i2p**
   2. If you do not have an http proxy block setup you can copy and paste this entire block below.

```
[httpproxy]
port = 4444
outproxy = http://exit.stormycloud.i2p
```

3. You will want to restart I2PD and that is all!

```
systemctl restart i2pd
```
