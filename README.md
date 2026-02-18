# LiveKit Setup - Port Requirements

This project contains a LiveKit setup using Docker Compose. Below is a detailed list of all ports used by the installation. Please ensure these ports are opened on the firewall/security groups to allow proper operation.

## External Ports (Must be open to public)

These ports are used for client connections and media streaming.

| Port            | Protocol | Service | Purpose                           |
| :-------------- | :------- | :------ | :-------------------------------- |
| **443**         | TCP      | Caddy   | HTTPS/TLS (API, WebSockets, WHIP) |
| **7881**        | TCP      | LiveKit | RTC (TCP fallback)                |
| **50000-60000** | UDP      | LiveKit | RTC (UDP media traffic)           |
| **3478**        | UDP      | TURN    | TURN (STUN/TURN media relay)      |
| **1935**        | TCP      | Ingress | RTMP ingest                       |
| **7885**        | UDP      | Ingress | Ingress RTC                       |
| **5060, 5070**  | TCP/UDP  | SIP     | SIP Signaling (5070 for Exotel)   |
| **10000-40000** | UDP      | SIP     | RTP Media Traffic                 |

## Internal Ports (Should NOT be exposed publicly)

These ports are used for internal communication between services or proxied by Caddy.

| Port     | Protocol | Service | Purpose                               |
| :------- | :------- | :------ | :------------------------------------ |
| **7880** | TCP      | LiveKit | HTTP/WebSocket API (Internal/Proxied) |
| **5349** | TCP      | TURN    | TURN TLS (Internal/Proxied)           |
| **8080** | TCP      | Ingress | WHIP (Internal/Proxied)               |
| **9090** | TCP      | Ingress | HTTP Relay (Internal)                 |
| **6379** | TCP      | Redis   | Redis Backend (Internal Only)         |

> [!IMPORTANT]
> LiveKit requires a large range of UDP ports (**50000-60000**) for media streaming. Ensure this range is fully open to the public to prevent connection issues.
