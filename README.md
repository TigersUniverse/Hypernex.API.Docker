# Hypernex.API.Docker

## Notes

- This is mainly for use on local/development/single-node servers.
- - Minio is configured to use a default username and password. This can be changed in `docker-compose.yml` via the environment variables. See Minio's documentation if needed.
- This will setup (almost) everything for you in one docker compose file.
- Port `80`, `2096`, `5000-5010`, `6379`, `27017`, `9000`, `9001` will be used by default.

## Setup

Make sure to install Docker or Docker Desktop. WSL is required on Windows.

Clone the repository with:
```bash
git clone https://github.com/TigersUniverse/Hypernex.API.Docker.git
```

Change directory:
```bash
cd Hypernex.API.Docker
```

Clone the API, Networking, And Web repositories:
```bash
git clone https://github.com/TigersUniverse/Hypernex.API.git API
git clone https://github.com/TigersUniverse/Hypernex.Networking.git Networking
git clone https://github.com/TigersUniverse/Hypernex.Web.git Web
```

## Configs Part 1

Change everything inside `<` and `>` brackets that you can. All configs go inside the `configs` folder next to this `README.md`. You may need to create the `configs` folder.

### Web API

Create a `config.json` for the Web API config in the `configs` folder. A template/example can be found in `configs/example.config.json`.

Be sure to remove the `// !!DO NOT change!!` from the `config.json` to prevent loading errors.

If you are using Godot as the Game Engine, use the full release tag in the release name. Example:

- `4.3-stable` -> `https://github.com/godotengine/godot-builds/releases/tag/4.3-stable`
- `4.2.2-stable` -> `https://github.com/godotengine/godot-builds/releases/tag/4.2.2-stable`

### Networking Server

Create a `serverconfig.cfg` for the Networking Server config in the `configs` folder. A template/example can be found in `configs/example.serverconfig.cfg`.

## Building

Build the Docker images (this will take some time on first run)
```bash
docker compose build
```

Start the containers
```bash
docker compose up -d
```

## Configs Part 2

### Minio

With the server running, visit the server with the port `9001` in a web browser. (for example, `http://localhost:9001`).

Login with the username and password (default is `minioadmin` and `minioadmin`).

Create a bucket with default settings and use the name in the `configs/config.json` file.

Create an access key with default settings and use the `Access Key` and `Secret Key` in `configs/config.json`

Change Server location in the `Configuration -> Region -> Server Location` tab and `configs/config.json`.

### Restart the Docker Containers

```bash
docker compose restart
```

## Final Notes

That's it! You should be all setup and ready to go!
