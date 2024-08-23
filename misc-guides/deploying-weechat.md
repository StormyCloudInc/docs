---
description: Guide meant for internal use but might be helpful for others
---

# Deploying Weechat

Install Weechat Repo\


```
sudo mkdir /root/.gnupg
sudo chmod 700 /root/.gnupg
sudo mkdir -p /usr/share/keyrings
sudo gpg --no-default-keyring --keyring /usr/share/keyrings/weechat-archive-keyring.gpg --keyserver hkps://keys.openpgp.org --recv-keys 11E9DE8848F2B65222AA75B8D1820DB22A11534E
echo "deb [signed-by=/usr/share/keyrings/weechat-archive-keyring.gpg] https://weechat.org/ubuntu jammy main" | sudo tee /etc/apt/sources.list.d/weechat.list
echo "deb-src [signed-by=/usr/share/keyrings/weechat-archive-keyring.gpg] https://weechat.org/ubuntu jammy main" | sudo tee -a /etc/apt/sources.list.d/weechat.list
sudo apt-get update
sudo apt-get install weechat-curses weechat-plugins weechat-python weechat-perl
```

Add IRC Server to Weechat

```
/server add i2p serverinfo/port
/set irc.server.i2p.nicks "Nick1,Nick2"
/set irc.server.i2p.autoconnect on
/set irc.server.i2p.command "/msg nickserv identify xxxxxxx"
/set irc.server.i2p.autojoin "#channel1,#channel2"

```

Installing SSL Cert

```
ufw disable
apt install certbot
mkdir -p /root/.config/.weechat/ssl
cat /etc/letsencrypt/live/irc.stormycloud.org/{fullchain,privkey}.pem > /root/.config/.weechat/ssl/relay.pem
chown -R root:root /root/.config/.weechat/ssl
```

Enabling SSL in Weechat

```
/set relay.network.password y0ur_StRonG-pa$sw0rd:of*choice
/relay tlscertkey
/relay add tls.weechat 9001
```

Hiding Part/Quit Messages

```
/set irc.look.smart_filter on
/filter add irc_smart * irc_smart_filter *
```
