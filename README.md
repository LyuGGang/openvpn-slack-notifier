OpenVPN-Slack-Notifier
=======

![Screenshot of Feature](screenshot.png)

This codes help to notify new connection of clients from [OpenVPN](https://openvpn.net/) to [Slack](https://slack.com) using post-auth and incoming-webhook. 
Since [server-side scripting with `client-connect` option deprecated](https://openvpn.net/vpn-server-resources/explanation-of-client-side-scripting-with-simple-examples/) on OpenVPN, we should use [post-auth](https://openvpn.net/vpn-server-resources/post-auth-programming-notes-and-examples/) feature instead. This codes referenced [this sample code](http://swupdate.openvpn.net/scripts/post_auth_mac_address_checking.py).

- - - 

Installation
---

#### Slack Configuration

1. Integrate `Incoming Webhooks` application into your Slack workspace. ([Guide Page](https://api.slack.com/custom-integrations/incoming-webhooks))
2. Add configurations on `Incoming Webhooks` as you want and beautify the icon and name of bot. :-)
3. Copy `Webhook URL` (Most important)

#### OpenVPN Configuration

1. Clone or Download `post_auth_slack_notifier.py` file from this repository to your OpenVPN server.
2. Open the `post_auth_slack_notifier.py` with editor and amend `WEBHOOK_URL` variable with value which you copied already like below.
   ```python
   # MODIFY THIS!!!!!!!!!!!
   WEBHOOK_URL = 'https://hooks.slack.com/services/XXXXXXXX/XXXXXXXX/XXXXXXXXXXXXXXXXX'
   ```
3. Add post-auth step using `sacli` like below.
   ```bash
   $ sudo su
   # cd /usr/local/openvpn_as/scripts  # assume that you have default settings
   # ./sacli -k auth.module.post_auth_script --value_file=/root/post_auth_slack_notifier.py ConfigPut  # assume that you downloaded file into /root/ directory
   # ./sacli start
   ```
4. (Optional) If you want remove(uninstall) settings or modify source files.
   ```bash
   $ sudo su
   # cd /usr/local/openvpn_as/scripts  # assume that you have default settings
   # ./sacli -k auth.module.post_auth_script ConfigDel
   # ./sacli start
   ```

License
---
Released under [WTFPL](http://www.wtfpl.net/about/) without warranty of any kind.