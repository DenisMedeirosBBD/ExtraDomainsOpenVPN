# ExtraDomainsOpenVPN
Overwriting domains to an OpenVPN connection that was added via NetworkManager

## How To

1. After adding your OpenVPN connection using NetworkManager, a config file will be created in the folder `/etc/NetworkManager/system-connections/<connection-name>`.
2. Edit the file above and make sure you have blocks `ipv4` and `ipv6` with the options `dns-search` set with all domains you want to overwrite (separated by semicolons). For example, for the domains `mydomain.lan` and `mydomain.zone`, it should look like:

```
[ipv4]
dns-search=mydomain.lan;mydomain.zone
method=auto
never-default=true

[ipv6]
addr-gen-mode=stable-privacy
dns-search=mydomain.lan;mydomain.zone
method=auto
never-default=true
```

3. Finally, restart the NetworkManager service and reconnected to your VPN.

```bash
systemctl restart NetworkManager
```

**Extra note:**

You can also check how the sytemd-resolved looks like by running:

```
systemd-resolve --status
```
The output for your connection should be similar to:

```
Link 43 (tun1)
      Current Scopes: DNS
       LLMNR setting: yes
MulticastDNS setting: no
      DNSSEC setting: no
    DNSSEC supported: no
         DNS Servers: 192.168.1.1
                      192.168.1.2
          DNS Domain: mydomain.lan
                      mydomain.zone
```                      
