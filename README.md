# Portainer Stacks
Created this repo because I was tired of losing those compose files and having to rewrite everything from scratch. There's a option in portainer that auto updates the stack directly from a git remote repository and polls at a configurable rate. Those are simpleass compose files using linuxserver images whenever possible. There are multiple .yml files because (in my experience) it's better than chugging everything into a single file or stack.
## Recommendations: 
* Is not advisable to use plex as remote git stack in portainer because the claim authentication is not gonna work.
* Remember to change the paths to your user instead of mine or any path you want. Just remeber that if not in home user folder you have to deal with permissions in linux, this is the easier way (not safer).
![example](https://github.com/rodhfr/portainer-stacks/blob/main/assets/Control-V.png)

