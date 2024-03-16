# Hypernex.API.Docker

## Notes

- This is mainly for use on local/development/single-node servers.
- - Minio is configured to use a default username and password. This can be changed in `docker-compose.yml` via environment variables. See Minio's documentation.
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

Change everything inside `<` and `>` brackets that you can, some configs will need to be filled in later in the guide.

### Web API

Create a `config.json` for the Web API config. Example:

```json
{
    "BaseURL": "http://localhost",
    "DatabaseInfo": {
        "DatabaseNumber": 0,
        "Host": "redis-server", // !!DO NOT change!!
        "Port": 6379,
        "Username": "",
        "Password": "",
        "UseDatabaseTLS": false,
        "DatabaseTLS": {
            "TLSKeyLocation": "",
            "TLSCertificateLocation": "",
            "TLSCALocation": ""
        }
    },
    "MongoDBURL": "mongodb://mongodb-server", // !!DO NOT change!!
    "SpacesInfo": {
        "AccessKeyId": "<access key from minio>",
        "SecretAccessKey": "<secret access key from minio>",
        "Region": "<minio access key>",
        "SpaceName": "<minio bucket name>",
        "ConnectionURL": "http://minio-server:9000" // !!DO NOT change!!
    },
    "MaxFileSize": 1000,
    "TrustAllDomains": false,
    "AllowedDomains": [],
    "UseHTTPS": false,
    "HTTPSTLS": {
        "TLSKeyLocation": "",
        "TLSCertificateLocation": ""
    },
    "SocketPort": 2096,
    "WebRoot": "../Web",
    "HTMLPaths": {
        "EmailVerificationPath": "emailhtml/verifyEmail.html",
        "ResetPasswordPath": "emailhtml/resetPassword.html"
    },
    "SignupRules": {
        "RequireInviteCode": false,
        "GlobalInviteCodes": [],
        "RemoveCodeAfterUse": true
    },
    "AVSettings":{
        "ScanFiles": false,
        "clamdPort": null,
        "clamdHost": null,
        "clamdTimeout": null,
        "clamdHealthCheckInterval": null
    },
    "GameServerTokens": ["<random token for game servers>"],
    "AllowAnyGameServer": false,
    "RequireTokenToDownloadBuilds": false,
    "GameEngine": "Unity",
    "GameEngineVersion": "2023.1.10f1"
}
```

### Networking Server

Create a `serverconfig.cfg` for the Networking Server config. Example:

```toml
# The server domain to connect to
ServerDomain = "hypernex-api" # !!DO NOT change!!
# Defines if the Server is HTTP
IsServerHTTP = true # !!DO NOT change!!
# Defines if the Server is WS
IsServerWS = "v1"
# GameServer Token; leave Empty if one isn't needed
GameServerToken = "<random token for game servers>"
# The Local IP Address for servers to run on
LocalIp = "0.0.0.0"
# The IP to be shared to the Socket Server
GlobalIp = "127.0.0.1"
# Beginning Port Range for GameServer's Instances
BeginPortRange = 5000
# Ending Port Range for GameServer's Instances
EndPortRange = 5010
# Have Instances use multiple Threads (recommended on)
UseMultithreading = true
# Time for threads to update (in ms)
ThreadUpdate = 10
# Allow IPs from IPV6 to connect
UseIPV6 = false
```

## Building

Build the Docker images
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

Create a bucket with default settings and use the name in the `config.json` file.

Create an access key with default settings and use the `Access Key` and `Secret Key` in `config.json`

Change Server location in the `Configuration -> Region -> Server Location` tab and `config.json`.

## Rebuild and restart the Docker Images and Containers

```bash
docker compose down
docker compose build
docker compose up -d
```
