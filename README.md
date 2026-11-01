## 👋 Welcome to standardnotes 🚀

End-to-end encrypted note-taking application

## 📋 Description

Standard Notes is an end-to-end encrypted note-taking service. The server only
ever sees ciphertext, notes are encrypted and decrypted in the client. This
stack runs the `standardnotes/server` image with a MariaDB database and a Redis
cache, with the API published on the host nginx proxy.

## 🚀 Services

- **app**: standardnotes/server:latest

### Infrastructure Components

- **standardnotes-db**: MariaDB database
- **standardnotes-redis**: Redis cache

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/standardnotes/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/standardnotes" ~/.local/srv/docker/standardnotes
cd ~/.local/srv/docker/standardnotes
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install standardnotes
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
DB_USER_NAME=standardnotes
DB_USER_PASS=replace-with-a-random-password
DB_ADMIN_PASS=replace-with-a-random-password
APP_SECRET_KEY=replace-with-a-random-32-byte-hex-string
PUBLIC_FILES_SERVER_PORT=3125
```

`APP_SECRET_KEY` becomes `AUTH_JWT_SECRET` inside the container and signs the
client auth tokens. `PUBLIC_FILES_SERVER_PORT` is baked into
`PUBLIC_FILES_SERVER_URL`, the address clients use to fetch file attachments
from the separate files server.

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64353` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64353

Point a Standard Notes client at this address. The API is served on container
port 3000.

## 📂 Volumes

- `./volumes/config/standardnotes` - Server configuration
- `./volumes/data/standardnotes` - Server data
- `./volumes/db/mariadb/standardnotes` - Database data
- `./volumes/db/redis/standardnotes` - Redis data

## 🔐 Security

- Set `APP_SECRET_KEY` to a random value of at least 32 characters, it signs
  the auth tokens clients present
- Change `DB_USER_PASS` and `DB_ADMIN_PASS` before the first start
- Notes are encrypted client side, so a database dump does not expose content
  but the server holds decryption-adjacent metadata
- Use HTTPS via the reverse proxy in production
- MariaDB and Redis are reachable only on the internal project network, no
  ports are published for them
- Keep `./volumes/db/mariadb/standardnotes` on a backed-up volume
- Regularly update Docker images for security patches

## 🔍 Logging

```shell
docker compose --env-file .env logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
