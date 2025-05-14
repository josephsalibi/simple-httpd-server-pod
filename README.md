# simple-httpd-server-pod

## This is an instructional repository only. No file content

## Summary
A simple pod driven HTTPD server setup utilizing podman, allowing you to host files and images such as iso's for consumption by other systems on your network.

## Requirements and Environmental Notes
The instructions below were last tested on Fedora 38 and applicable to similar operating systems.

It is assumed that the base OS is a linux system with podman and systemd functionality preinstalled/pre-existing.

You may need to consider firewalling and networking complexities for your particular base OS.

The image used and pulled for this execution was docker.io/library/httpd:2.4 but would recommend you use latest for up to date bug and security fixes (docker.io/library/httpd:latest)

## HTTPD SERVER
1. Create Directory
> mkdir /var/shared/httpd

2. Run httpd pod:
> podman run --name httpd -d -p 8100:80/tcp -v "/var/shared/containers/httpd/:/usr/local/apache2/htdocs/:z" httpd

3. Create the systemd service and apply it
> podman generate systemd --new --files --name httpd

> mv container-httpd.service /etc/systemd/system/

> systemctl enable container-httpd.service

> systemctl start container-httpd.service

4. Load any files to be offered by httpd server by copying any files to:
> /var/shared/httpd/
