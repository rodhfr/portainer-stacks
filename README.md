# Portainer Stacks
Created this repo because I was tired of losing those compose files and having to rewrite everything from scratch. There's a option in portainer that auto updates the stack directly from a git remote repository and polls at a configurable rate. Those are simpleass compose files using linuxserver images whenever possible. There are multiple .yml files because (in my experience) it's better than chugging everything into a single file or stack.
![example](https://github.com/rodhfr/portainer-stacks/blob/main/assets/Control-V.png)
## Recommendations: 
* Is not advisable to use plex as remote git stack in portainer because the claim authentication is not gonna work.
* Remember to change the paths to your user instead of mine or any path you want. Just remeber that if not in home user folder you have to deal with permissions in linux, this is the easier way (not safer).
* Clone this repo and do your thing

## STEPS
1) On a fresh machine install docker
> [!NOTE] 
> This is archlinux docker installation look up for your distro, albeit they are similar.
```bash
yay -Syu docker```
[post install steps docker](https://docs.docker.com/engine/install/linux-postinstall/)
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
2) Install portainer
```bash
docker volume create portainer_data
docker run -d -p "127.0.0.1:8000:8000" -p "127.0.0.1:9443:9443" --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:2.21.4
```
3) Create portainer login
4) Load stacks from portainer
