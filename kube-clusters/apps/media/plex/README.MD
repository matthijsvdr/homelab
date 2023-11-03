For plex in kubernets to realise it has a local connection all plex.direct domains needs to point to the ingress and from there with a TCP connection passed through to plex itself. See [pihole](#pihole-example)



Idea

Have plex run on a hostnetwork but still have a proxy in place for mvd.sh domain, then plex clients can contact it locally

### pihole example

```ini
server=/plex.direct/10.20.10.10
address=/plex.direct/10.20.10.10
```

```
Login to your pi-hole and go to /etc/dnsmasq.d/
Create a new file, lets call it 02-my-wildcard-dns.conf
Edit the file, and add a line like this:

address=/mydomain.lab/192.168.1.20

Save the file, and exit the editor
Run the command: service pihole-FTL restart

https://hetzbiz.cloud/2022/03/04/wildcard-dns-in-pihole/
```
