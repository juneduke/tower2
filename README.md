# Tower Dashboard

Tower is a custom apparatus designed and built by Junhee Won, an undergraduate scientist and engineer in KAIST. **Tower Dashboard** is supporting service of Tower, providing control of extruder/fiber motors and heater via web service.

Tower Dashboard is developed for Raspberry Pi with Docker.

## Installation

1. Install Docker and Docker Compose.
2. Clone repository
3. Set up `.env` file.
4. `docker-compose up -d`

**Set up `.env` file**

Copy `.env.dist` to `.env`, and fill values.

| Variable            | Example        | Description                                        |
| ------------------- | -------------- | -------------------------------------------------- |
| EMAIL               | ex@amp.le      | Email address for Let's Encrypt HTTPS certificate. |
| HOST                | example.net    | Host server address.                               |
| TOWER_HEATER_PORT   | `/dev/ttyUSB0` | Heater USB port.                                   |
| TOWER_EXTRUDER_PORT | `/dev/ttyACM0` | Extruder USB port.                                 |
| TOWER_FIBER_PORT    | `/dev/ttyACM1` | Fiber USB port.                                    |

## Implementation

Tower Dashboard is composed of two Docker containers, one is Traefik reverse proxy and the other is Flask  web server. Traefik is introduced for simple Let's Encrypt certificate management.

## Previous works

This project is created as a replacement of [tower-server](https://github.com/EOMMINHO/tower-server.git) worked by [EOMMINHO](https://github.com/EOMMINHO). The need of replacement is introduced to change the server from a PC to Raspberry Pi, since using a PC solely for this very light service is wasting too much hardware resource.

We brought arduino-side code and communication protocol unchanged, which may differ in future.

## Future Works

#### USB identification

Currently, device mapping is not located automatically, and hardcoded in `.env` by hand. We'll resolve this by implementing identification step in communication protocol so that arduino tells which it is.

#### Soft limit

Master would be able to change the limit range of device value(speed or temperature) in future. Currently they're hardcoded.