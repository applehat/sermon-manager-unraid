# Sermon Manager for Unraid

Unraid does not install this repository from a URL. The Docker settings page has no Template repositories field, and Add Container does not load a raw XML URL. Type the container in by hand. The values below match `templates/sermon-manager.xml`.

This is a church LAN app. There is no login. Do not expose it to the internet.

1. Open Docker.
2. Click Add Container.
3. Turn on Advanced View. WebUI and Extra Parameters are on that view. Name, Repository, and Network Type are already on the form.
4. Name: `Sermon-Manager`. The Name box accepts only letters, numbers, `.`, `_`, and `-`. `Sermon Manager` (the name in the XML) contains a space and the form will not submit it.
5. Repository: `ghcr.io/applehat/sermon-manager:latest`
6. Leave Network Type on Bridge.
7. WebUI: `http://[IP]:[PORT:8080]/`
8. Extra Parameters: `--stop-timeout 600`
9. Leave Privileged off.
10. Click Add another Path, Port, Variable, Label or Device once for each row below. Set Config Type, then the two boxes named in that row. Use Read/Write for the path and TCP for the port. Click Add.
11. Click Apply.
12. Open the WebUI and use Settings. That page is where Whisper, Ollama, YouTube, Facebook, and Spotify are configured. Nothing in that list is a container variable.

Port:

- Config Type Port. Name `WebUI`. Container Port `8080`. Host Port `8080`. Connection Type TCP.

Path. One folder. The app creates `data/`, `media/`, `secrets/`, and `settings.json` inside it.

- Config Type Path. Name `Sermon Root`. Container Path `/sermons`. Host Path `/mnt/user/appdata/sermon-manager`. Access Mode Read/Write. SQLite is `data/sermons.db`. Uploads are in `media/`. Settings are in `settings.json`. YouTube and Spotify JSON files are in `secrets/`, and that directory must stay writable.

Do not add a variable. Do not build an image on Unraid. Do not install this from Community Apps.

The Docker page shows an update when a new image is pushed to the latest tag. That update does not add a port or path. Edit the container, or remove it and add it again.
