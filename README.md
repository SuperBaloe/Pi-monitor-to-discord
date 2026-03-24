# Pi Monitor to Discord

## Libraries

### Built-in
- `os`
- `time`
- `json`
- `datetime`
- `socket`

### Installed
- `requests`
- `psutil`
- `questionary`

## Features

Posts your machine CPU and RAM usages and uptime to Discord chat.

![Discord Update](https://github.com/user-attachments/assets/6bcc596f-9da4-49d1-8d3d-f4609d5eb7cb)

## Usage

The whole program can be used in the terminal and automatically creates its own config and message ID file.

### Main Menu
![Main Menu](https://github.com/user-attachments/assets/b26a9f80-0979-4ea9-978d-1adeb656004a)

### Configuration
![Configuration](https://github.com/user-attachments/assets/e21e763d-d10e-4ff0-81ad-0ed4b7e928be)

## Running as a Linux Service

You can run Pi Monitor to Discord as a systemd service that automatically starts on boot.

### Setup Instructions

1. **Create a systemd service file:**

```bash
sudo nano /etc/systemd/system/pi-monitor-discord.service
```

2. **Add the following configuration** (replace `/path/to/` with your actual installation path and `your_user` with your username):

```ini
[Unit]
Description=Pi Monitor to Discord
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
User=your_user
WorkingDirectory=/home/your_user/Pi-monitor-to-discord
ExecStart=/usr/bin/python3 /home/your_user/Pi-monitor-to-discord/machine_monitoring.py --service
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

3. **Reload systemd and enable the service:**

```bash
sudo systemctl daemon-reload
sudo systemctl enable pi-monitor.service
sudo systemctl start pi-monitor.service
```

### Service Management Commands

- **Check service status:**
```bash
sudo systemctl status pi-monitor-discord.service
```

- **View service logs:**
```bash
sudo journalctl -u pi-monitor-discord.service -f
```

- **Stop the service:**
```bash
sudo systemctl stop pi-monitor-discord.service
```

- **Restart the service:**
```bash
sudo systemctl restart pi-monitor-discord.service
```

### Notes

- Make sure to configure the application first by running it manually before setting it up as a service
- The service will automatically restart if it crashes (with a 10-second delay)
- Logs can be viewed using `journalctl` for debugging
- The service runs as the specified user, so ensure they have proper file permissions
