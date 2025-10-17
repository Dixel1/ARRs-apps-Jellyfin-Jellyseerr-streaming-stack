# ARRs-apps-Jellyfin-Jellyseerr-streaming-stack
A simple way to deploy your own streaming stack with ARRs apps, Jellyfin &amp; Jellyseerr.

## Components
- **ARRs apps**: A collection of reverse proxy applications to manage and route traffic
    - **Prowlarr**: A web application that integrates with various indexers for media content.
    - **Radarr**: A movie collection manager for downloading and organizing movies.
    - **Sonarr**: A TV series collection manager for downloading and organizing TV shows.
- **Jellyfin**: An open-source media server for streaming your personal media.
- **Jellyseerr**: A self-hosted media request management tool for Jellyfin.
- **Traefik**: A modern reverse proxy and load balancer.
### Bonus
- **Dockge**: A web-based Docker management tool.

## Prerequisites
- Docker and Docker Compose installed on your server.
- A domain name with DNS records pointing to your server.
- Basic knowledge of Docker and reverse proxies.

## Setup Instructions
1. **Clone the Repository**
   ```bash
   git clone https://github.com/yourusername/ARRs-apps-Jellyfin-Jellyseerr-streaming-stack.git
   cd ARRs-apps-Jellyfin-Jellyseerr-streaming-stack
    ```
2. **Configure Environment Variables**
   Copy the `.env` file and update the variables as needed.
   ```bash
   cp .env /your/path/to/.env
   ```

3. **Start the Services**
   Use Docker Compose to start the services.
   ```bash
   docker-compose up -d
   ```

4. **Stop the Services (WITHOUT DESTROYING DATA)**
   To stop the services, run:
   ```bash
   docker-compose down
   ```