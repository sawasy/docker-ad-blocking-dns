docker-ad-blocking-dns
======================
*docker-ad-blocking-dns* is an Ubuntu  container with bind9 and IP blacklisting

```shell
cd docker-ad-blocking-dns
sudo docker build -t sawasy/docker-ad-blocking-dns
sudo docker run -d -p 53:53 sawasy/docker-ad-blocking-dns
```
###Notes
You can tweak a few things. If you swap the 127.0.0.1 reference, in null.zone.file, for a real webserver you can track the 404s there. 

Also, you might want to disable 
```shell
'allow-query-cache { any; };'
```
in named.conf.options if you are on a public network. Or not. Up to you.


This could be setup as a container on your workstation. Editing /etc/resolv.conf
```shell
nameserver localhost
```
will likely do the trick.

If you are doing this on an Ubuntu workstation, you likely will need to disable dnsmasq.
```shell
sudo sed -i -e 's/dns=dnsmasq/#dns=dnsmasq/g' /etc/NetworkManager/NetworkManager.conf
```
###Reference
Most of the heavy lifting for this was sorted out here: http://www.lituxx.com/website/en/2014/03/block-ads-on-your-entire-network/

Also, this uses the excellent Advertiser black list at http://pgl.yoyo.org/as/

