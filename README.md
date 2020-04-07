openfortivpn
============

We use these files to create the
[_openfortivpn_ snap](https://snapcraft.io/openfortivpn) from the
[_openfortivpn_ sources](https://github.com/adrienverge/openfortivpn).

openfortivpn is a client for PPP+SSL VPN tunnel services.
It spawns a pppd process and operates the communication between the gateway and
this process.

It is compatible with Fortinet VPNs.


------------
Installing
------------

Install the snap from the [Snap Store](https://snapcraft.io/store):
```
sudo snap install openfortivpn
```

Until the _openfortivpn_ snap is authorized to auto-connect, you need to 
connect these two _plugs_ manually:
```
sudo snap connect openfortivpn:ppp
sudo snap connect openfortivpn:network-control
```


------------
Examples
------------

* Simply connect to a VPN:
  ```
  sudo openfortivpn vpn-gateway:8443 --username=foo
  ```

* Connect to a VPN using an authentication realm:
  ```
  sudo openfortivpn vpn-gateway:8443 --username=foo--realm=bar
  ```

* Don't set IP routes and don't add VPN nameservers to `/etc/resolv.conf`:
  ```
  openfortivpn vpn-gateway:8443 -u foo -p bar --no-routes --no-dns --pppd-no-peerdns
  ```

* Using a config file:
  ```
  openfortivpn -c /snap/openfortivpn/common/config
  ```

  With `/var/snap/openfortivpn/common/config` containing:
  ```
  host = vpn-gateway
  port = 8443
  username = foo
  password = bar
  set-routes = 0
  set-dns = 0
  pppd-use-peerdns = 0
  # X509 certificate sha256 sum, trust only this one!
  trusted-cert = e46d4aff08ba6914e64daa85bc6112a422fa7ce16631bff0b592a28556f993db
  ```
