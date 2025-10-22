# ARRs-apps-Jellyfin-Jellyseerr-streaming-stack
A simple way to deploy your own streaming stack with ARRs apps, Jellyfin &amp; Jellyseerr.

## Components
- **ARRs apps**: A collection of applications for managing and automating media downloads.
    - **Prowlarr**: A web application that integrates with various indexers for media content.
    - **Radarr**: A movie collection manager for downloading and organizing movies.
    - **Sonarr**: A TV series collection manager for downloading and organizing TV shows.
- **Jellyfin**: An open-source media server for streaming your personal media.
- **Jellyseerr**: A self-hosted media request management tool for Jellyfin.
- **Traefik**: A modern reverse proxy and load balancer.
- **qBittorrent**: A lightweight and efficient BitTorrent client.

### Bonus
- **Dockge**: A web-based Docker management tool.

## Prerequisites
- Docker and Docker Compose installed on your server.
- A domain name with DNS records pointing to your server.
- Basic knowledge of Docker and reverse proxies.

## Setup Instructions
1. **Clone the Repository**
   ```bash
   git clone https://github.com/Dixel1/ARRs-apps-Jellyfin-Jellyseerr-streaming-stack.git
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

5. **Troubleshooting**
   - Check the logs of individual services using:

   ```bash
   docker-compose logs <service_name>
   ```

   - Ensure that your DNS records are correctly set up and pointing to your server.
   - Verify that the ports required by each service are open and not blocked by a firewall.
   - Consult the documentation of each component for specific configuration options and troubleshooting tips. You can fiend them here:
     - [Prowlarr Documentation](https://wiki.servarr.com/prowlarr)
     - [Radarr Documentation](https://wiki.servarr.com/radarr)
     - [Sonarr Documentation](https://wiki.servarr.com/sonarr)
     - [Jellyfin Documentation](https://jellyfin.org/docs/)
     - [Jellyseerr Documentation](https://jellyseerr.com/docs/)
     - [Traefik Documentation](https://doc.traefik.io/traefik/)
     - [Dockge Documentation](https://dockge.com/docs/)

   ## Mounting Volumes
   Ensure that you have the necessary directories created on your host machine for data persistence.

   In this setup, external volumes for data are mounted to the following paths inside the containers /mnt/externalusb/data/

   The arborescence should look like this:

   ``` 
   data
   ├── torrents
   │   ├── movies
   │   └── tv
   └── media
       ├── movies
       └── tv
   ```

## ⚠️ WARNING - Permission Issues on Windows Formatted Drives

   If you're mounting a Windows formatted drive (like NTFS or exFAT), you may encounter permission issues. For better compatibility, consider using ext4 formatted drives.

   If you ABSOLUTELY want to use a Windows formatted drive on a Linux system read the following.

   ### For NTFS
   1. You may need to use `ntfs-3g` package:
   ```bash
   sudo apt install ntfs-3g
   lsblk -f
   ```

   2. Then mount the drive with appropriate options (here sdb1 is an example, replace it with your actual device):
   ```bash
   sudo mount -t ntfs-3g /dev/sdb1 /mnt/externalusb -o uid=1000,gid=1000,umask=002
   ```
   
   3. Verify mount point with:
   ```bash
   mount | grep externalusb
   ```

   ### For exFAT drives
   1. You can use `exfat-fuse` and `exfat-utils` packages:
   ```bash
   sudo apt install exfat-fuse exfat-utils
   lsblk -f
   ```

   2. Then mount the drive with appropriate options (here sdb1 is an example, replace it with your actual device):
   ```bash
   sudo mount -t exfat /dev/sdb1 /mnt/externalusb -o uid=1000,gid=1000,umask=002
   ```
   3. Verify mount point with:
   ```bash
   mount | grep externalusb
   ```

   ### (Optional) To make the mount permanent, add an entry to `/etc/fstab`:
   ```
   # For NTFS
   /dev/sdb1 /mnt/externalusb ntfs-3g uid=1000,gid=1000,umask=002 0 0

   # For exFAT
   /dev/sdb1 /mnt/externalusb exfat defaults,uid=1000,gid=1000,umask=002 0 0
   ```
