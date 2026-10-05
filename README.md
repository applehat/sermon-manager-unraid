# Sermon Manager for Unraid

Install Sermon Manager from this template repository. One container, image `ghcr.io/applehat/sermon-manager:latest`.

This is a church LAN app. There is no login. Do not expose it to the internet.

1. Open Settings.
2. Open Docker.
3. Turn on Advanced View.
4. Find Template repositories.
5. Paste https://github.com/applehat/sermon-manager-unraid
6. Click Save.
7. Open Docker.
8. Click Add Container.
9. Choose Sermon Manager from the template dropdown.
10. Set the paths and optional hosts.
11. Click Apply.

The Docker page shows an update when a new image is pushed to the latest tag. A new port or path in the template is not applied by that update. Remove the template and add the container again.
