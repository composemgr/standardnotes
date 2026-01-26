## 👋 Welcome to standardnotes 🚀

End-to-end encrypted note-taking application

## 📋 Description

End-to-end encrypted note-taking application

## 🚀 Services

- **standardnotes**: standardnotes/standardnotes:latest

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/standardnotes/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/standardnotes" ~/.local/srv/docker/standardnotes
cd ~/.local/srv/docker/standardnotes
docker compose up -d
```

### Option 3: Using composemgr
```bash
composemgr install standardnotes
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
SERVICE_USER=1000
SERVICE_GROUP=1000
```

See `docker-compose.yaml` for complete list of configurable options.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:3000

## 📂 Volumes

- `./rootfs/config/standardnotes` - Data storage
- `./rootfs/data/standardnotes` - Data storage

## 🔍 Logging

```shell
docker compose logs -f standardnotes
```

## 🛠️ Management

```bash
# Start services
docker compose up -d

# Stop services
docker compose down

# Update to latest images
docker compose pull && docker compose up -d

# View logs
docker compose logs -f

# Restart services
docker compose restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
