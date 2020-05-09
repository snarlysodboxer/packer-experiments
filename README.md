# Let's learn some Packer

## Instructions
* Create a Packer template with the following criteria
  * Use the Docker Builder
  * Use Ansible, Puppet, or Shell Provisioner
  * Build from `ubuntu:latest` or a `centos:latest` based on an arg passed to the Packer CLI
  * Install Nginx, and configure it to serve static content from `/html/` on port 80
  * Push successfully built images to my personal Docker hub account

## Notes on my provided solution
* For something as simple as installing and configuring Nginx in this fashion, I see no sense in involving more sophisticated solutions than Bash.
* We've configured Nginx to run it's child processes as the `nginx` user, but many would want to disallow privileged users in the container via the security context. Since the requirement is to bind to port 80, we have to be root. An easy fix would be to bind to 8080 inside the container, and then bind that port to whatever port you want outside the container.

## Solution instructions
* `packer build -var 'base_image=ubuntu' packer-nginx.json`
* `packer build -var 'base_image=centos' packer-nginx.json`
* `docker run -it --rm -v ${PWD}:/html -p 8888:80 snarlysodboxer/ubuntu-nginx:latest`
* `docker run -it --rm -v ${PWD}:/html -p 8888:80 snarlysodboxer/centos-nginx:latest`

