# Media browser
## Browse movies and tv shows easily!


## Requirements

- Docker
- Docker Compose
- Curl
- Plex account and server
- nCore account
- TheMovieDB account (token)
- qBittorrent server instance to download media
- Telegram account (optional for notifications, bot token and chat id)

## Setup

Run the installer script
```
curl -s https://raw.githubusercontent.com/bdaviddvlp/media-browser/refs/heads/main/install | bash
```

## Configuration

### local.json
The filled out configuration file should remain unchanged, the empty fields should be filled out with your own data and credentials. The file should look like this:
```json
{
  "database": {
    "username": "",
    "password": "",
    "database": "media-browser",
    "host": "mongo",
    "port": "27017"
  },
  "plex": {
    "url": "",
    "libraries": {
      "movie": {
        "1": ""
      },
      "tv": {
        "2": ""
      },
      "music": {
        "3": ""
      }
    }
  },
  "tmdb": {
    "apiKey": ""
  },
  "cors": {
    "url": ""
  },
  "ncore": {
    "baseUrl": "https://ncore.pro",
    "username": "",
    "password": ""
  },
  "qbittorrent": {
    "baseUrl": "",
    "fileDownloadPath": {
      "movie": "",
      "tv": ""
    },
    "isDry": false
  },
  "admin": {
    "username": "",
    "email": "",
    "password": "",
    "isAdmin": true
  }
}

```
- database: MongoDB credentials, provide credentials as you prefer.
- plex: Plex server credentials. In the `libraries` field, you should provide library ID as key and filesystem path of the movies and tv shows. The primary keys e.g. `movie` should remain unchanged as they are used in the code to identify the type of media.
- tmdb: TMDB API key, you can get it from https://www.themoviedb.org/settings/api.
- cors: CORS URL, provide the URL of the CORS proxy you want to use.
- ncore: Ncore credentials.
- qbittorrent:
    - In the `fileDownloadPath` field, you should provide the path where you want to download the movies and tv shows.
    - The `isDry` field is used to test the download without actually downloading the file, leave it `false` to download the files.
    - To skip authentication for this app, you must set the internal ip address of the server where you run media-browser.
    - To do this, you can find the settings at `Tools > Options > Web UI > Bypass authentication for clients in whitelisted IP subnets`.
    - To update app cache and trigger plex library scan, you must set the webhook action when a torrent download finished.
    - In the settings at `Tools > Options > Downloads > Run external program on torrent finished`, set `qbittorrent_webhook_complete "%N" "%L" "%G" "%F" "%R" "%D" "%C" "%Z" "%T" "%I" "%J" "%K"`.
- admin: Admin credentials, it will be the web UI admin. Provide credentials as you prefer.

## .env
```
# Should match with the local.json values
MONGO_INITDB_ROOT_PASSWORD=
MONGO_INITDB_ROOT_USERNAME=
MONGO_INITDB_DATABASE=media-browser
JWT_SECRET=
# Optional for notifications
TELEGRAM_BOT_TOKEN=
TELEGRAM_CHAT_ID=
```