# Dedicated Minecraft Fabric Server Configuration

[![Platform: Fabric](https://img.shields.io/badge/Platform-Fabric_MC-black.svg?logo=curseforge)](https://fabricmc.net/)
[![Minecraft: 1.20+](https://img.shields.io/badge/Minecraft-1.20%2B-green.svg)](https://www.minecraft.net/)
[![Java: 17/21](https://img.shields.io/badge/Java-OpenJDK_17%2B-orange.svg?logo=openjdk)](https://adoptium.net/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Optimized server configuration, access control policies, mod loader setup, and administration templates for a dedicated Minecraft Fabric server.

## Description
This repository contains the configuration files, whitelist access controls, operator permission records, and deployment structure for running a high-performance modded Minecraft server on the Fabric loader. It is optimized for low tick overhead, efficient memory allocation, and reliable multi-player persistence.

### Key Features
* **Fabric Modding Ecosystem**: Lightweight mod loader architecture delivering near-vanilla performance while supporting server-side performance mods (Lithium, FerriteCore, Krypton).
* **Access Control Infrastructure**: Explicit configurations for whitelisted users (`whitelist.json`), operator permission levels (`ops.json`), and access bans (`banned-players.json`, `banned-ips.json`).
* **Optimized Java Runtime Flags**: Configured for modern garbage collectors (ZGC or G1GC with Aikar's tuning parameters) to prevent tick spikes and minimize garbage collection latency.
* **Persistent World Management**: Clean separation of configuration files from server world storage.

## Directory Structure
```text
MinecraftFabricServer/
├── banned-ips.json         # IP-level access restrictions
├── banned-players.json     # Player UUID security restrictions
├── ops.json                # Operator privilege definitions (Levels 1 through 4)
├── usercache.json          # Cached mapping of player names to Mojang UUIDs
├── whitelist.json          # Authorized player access whitelist
├── world/                  # Persistent Minecraft world directory (regions, data, entities)
└── README.md               # Server documentation and runbook
```

## Requirements
* Java Development Kit: OpenJDK 17 or OpenJDK 21
* Fabric Server Loader JAR (`fabric-server-launch.jar`)
* Minimum System RAM: 4 GB (8 GB recommended for 10+ concurrent players)

## Installation & Setup
1. Clone the configuration repository:
   ```bash
   git clone https://github.com/ADM1SH/MinecraftFabricServer.git
   cd MinecraftFabricServer
   ```
2. Download the official Fabric Server installer matching your Minecraft release:
   ```bash
   curl -OJ https://meta.fabricmc.net/v2/versions/loader/1.20.4/0.15.7/1.0.1/server/jar
   ```
3. Accept the Minecraft EULA by creating `eula.txt`:
   ```bash
   echo "eula=true" > eula.txt
   ```

## Usage
Start the Fabric server with high-performance JVM flags:
```bash
java -Xms4G -Xmx6G      -XX:+UseG1GC      -XX:+ParallelRefProcEnabled      -XX:MaxGCPauseMillis=200      -XX:+UnlockExperimentalVMOptions      -XX:+DisableExplicitGC      -XX:+AlwaysPreTouch      -jar fabric-server-launch.jar nogui
```

### Server Administration Commands
* Add player to whitelist: `whitelist add <PlayerName>`
* Promote player to operator: `op <PlayerName>`
* Force world save: `save-all`
* Safe server shutdown: `stop`

## Support
Open an issue on GitHub for server administration questions:
https://github.com/ADM1SH/MinecraftFabricServer/issues

## Roadmap
* [x] Configure Fabric loader and permission files.
* [x] Benchmark memory allocation with G1GC flags.
* [ ] Add automated hourly backup script with rsync/tar.
* [ ] Integrate DiscordSRV bot bridge for server chat integration.

## Contributing
1. Fork this repository.
2. Create a branch: `git checkout -b config/backup-cron`.
3. Submit a Pull Request with tested script modifications.

## Authors and Acknowledgment
* **Adam Anwar** (ADM1SH) - Server administrator and configuration architect.
* **FabricMC Project** - Lightweight mod loader development.

## License
MIT License. See `LICENSE` for details.

## Project Status
Maintained server configuration. Ready for deployment on local networks or remote VPS instances.
