# Portainer Stacks
Created this repo because I was tired of losing those compose files and having to rewrite everything from scratch. There's a option in portainer that auto updates the stack directly from a git remote repository and polls at a configurable rate. Those are simpleass compose files using linuxserver images whenever possible. There are multiple .yml files because (in my experience) it's better than chugging everything into a single file or stack.

 ![example](https://github.com/rodhfr/portainer-stacks/blob/main/assets/Control-V.png)
## Recommendations: 
* Is not advisable to use plex as remote git stack in portainer because the claim authentication is not gonna work.
* Remember to change the paths to your user instead of mine or any path you want. Just remeber that if not in home user folder you have to deal with permissions in linux, this is the easier way (not safer).
* Clone this repo and do your thing
* Everything is mapped to 127.0.0.1 this means it will only work on localhost not on lan network (192.168.0.100 and likes). This is ideal if you have a nginx-proxy setup because the servers could no longer be accessed through public ipv6
> [!TIP]
> Example IPV6 address with 8096 port:
> 
> **http://[2001:0db8:85a3:0000:0000:8a2e:0370:7334]:8096**
> 
This is due to docker writing to a new iptables and not being compatible with normal linux firewalls like ufw. 

> [!CAUTION]
> Meaning: Docker ignores normal computer firewall rules and let mapped ports open to the public by default. 

There is [workarounds](https://github.com/chaifeng/ufw-docker) for this but mapping to localhost is the easiest and less troublesome that I found. If you want to acess from local lan network then remove the 127.0.0.1 prefix from the ports. 

Example before "127.0.0.1:8096" and after "8096:8096".


![image](https://github.com/user-attachments/assets/0ae13adf-59c3-4e6a-bb06-6c9fe25fb0f6)
![image](https://github.com/user-attachments/assets/b689576b-c6b3-46e6-9cf3-b0edee07537a)

If you want to work with nginx-proxy-manager [RECOMMENDED] there is a [.yml](https://github.com/rodhfr/portainer-stacks/blob/main/nginx-proxy-manager.yml) file in this repo.

## STEPS
1) On a fresh machine install docker
> [!NOTE] 
> This is archlinux docker installation look up for your distro, albeit they are similar.
```bash
yay -Syu docker
```
2) [Post install steps docker](https://docs.docker.com/engine/install/linux-postinstall/)
```bash
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
docker run --rm hello-world
```
Start and enable docker via systemctl or others init systems 
```bash
sudo systemctl enable docker.service
sudo systemctl enable containerd.service```
To stop docker from start at startup
```bash
sudo systemctl disable docker.service
sudo systemctl disable containerd.service
```
3) Install portainer
```bash
docker volume create portainer_data
docker run -d -p "127.0.0.1:8000:8000" -p "127.0.0.1:9443:9443" --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:2.21.4
```
4) Create portainer login
5) Load stacks from portainer
6) Optional: configure nginx-proxy-manager and ddns cloudflare stack.
