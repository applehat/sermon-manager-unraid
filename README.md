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
10. Click Add another Path, Port, Variable, Label or Device once for each row below. Set Config Type, then the two boxes named in that row. Use Read/Write for paths and TCP for the port. Click Add.
11. Click Apply.

Port:

- Config Type Port. Name `WebUI`. Container Port `8080`. Host Port `8080`. Connection Type TCP.

Paths:

- Config Type Path. Name `App Data`. Container Path `/data`. Host Path `/mnt/user/appdata/sermon-manager`. Access Mode Read/Write. The database file is `/data/sermons.db`.
- Config Type Path. Name `Media`. Container Path `/media`. Host Path `/mnt/user/sermon-manager`. Access Mode Read/Write.
- Config Type Path. Name `Secrets`. Container Path `/secrets`. Host Path `/mnt/user/appdata/sermon-manager/secrets`. Access Mode Read/Write. YouTube and Spotify JSON files live here, and the path must stay writable.

Variables. Key is the variable name. Leave a value blank when the row says empty.

- `WHISPER_HOST`: empty. Optional host of whisper-asr-webservice. Empty leaves the transcript pending. Port defaults to 9000.
- `LLM_HOST`: empty. Optional host of Ollama. Empty uses an extractive summary. Port defaults to 11434.
- `YOUTUBE_CLIENT_SECRETS`: `/secrets/youtube_client_secret.json`
- `YOUTUBE_TOKEN_FILE`: `/secrets/youtube_token.json`
- `YOUTUBE_PRIVACY_STATUS`: `public`
- `YOUTUBE_CATEGORY_ID`: `22`
- `YOUTUBE_PLAYLIST_ID`: empty
- `FACEBOOK_PAGE_ID`: empty
- `FACEBOOK_PAGE_ACCESS_TOKEN`: empty. In the add-config popup, open the advanced section and set Password Mask to Yes.
- `FACEBOOK_GRAPH_VERSION`: `v26.0`
- `FACEBOOK_VIDEO_HOST`: `https://graph-video.facebook.com`
- `FACEBOOK_GRAPH_HOST`: `https://graph.facebook.com`
- `FACEBOOK_APP_ID`: empty
- `SPOTIFY_STORAGE_STATE`: `/secrets/spotify_state.json`
- `SPOTIFY_SHOW_URL`: `https://creators.spotify.com/dash/home`
- `SPOTIFY_HEADLESS`: `true`
- `SPOTIFY_UPLOAD_TIMEOUT_MS`: `3600000`

The Docker page shows an update when a new image is pushed to the latest tag. That update does not add a port or path. Edit the container, or remove it and add it again.
