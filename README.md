# Banned IPs Monitoring Script

This bash script monitors and displays the list of currently banned IP addresses from `fail2ban`, shows the time remaining until the IP is unbanned, and provides additional server statistics such as CPU load, disk usage, and memory usage.

## Features

- **List of Banned IPs**: Shows the current list of banned IP addresses using `fail2ban-client`.
- **Time Until Unban**: Calculates how many minutes are left until each IP is unbanned.
- **Server Information**: Displays the server's CPU load, temperature, disk usage, memory usage, and logged-in users.
- **Real-Time Monitoring**: Refreshes every minute to provide real-time updates.

## Requirements

- `fail2ban` must be installed and configured on the system.
- The script requires `sudo` privileges to access `fail2ban-client` and logs.
- Linux-based system with access to `/var/log/fail2ban.log`.
- Ensure that `bash` is used as the shell interpreter.

## Usage

1. **Make the script executable**:
    ```bash
    chmod +x monitor_banned_ips.sh
    ```

2. **Run the script with sudo**:
    ```bash
    sudo ./monitor_banned_ips.sh
    ```

   The script will continuously monitor and display:
   
   - **Currently Banned IPs**: A dynamic list of IP addresses banned via `fail2ban`.
   - **Unban Time**: Time remaining until each IP gets unbanned (default ban time assumed as 1 hour).
   - **Server Info**: CPU load, CPU temperature, disk usage, memory usage, logged-in users.

3. **Terminate the script**: The script will keep running indefinitely. To stop it, press `CTRL+C`.

## Output Example

```bash
 ┌─────┬──────────────────────┬───────────┐
 │ No. │          IP          │  Unban In │
 ├─────┼──────────────────────┼───────────┤
 │  1  │     192.168.1.100    │  10 mins  │
 │  2  │     172.16.0.5       │  45 mins  │
 └─────┴──────────────────────┴───────────┘

 - Server Info:
   - CPU Load : 0.50, 0.70, 0.60
   - CPU Temp : 45.2 °C
   - Disk Usage : 70%
   - Memory Usage : 1000/2000MB
   - Count of unique logged-in users : 2
   - Logged in as : user1, user2

  Current Time: 14:25:36
```

## Customization

- **Ban Time**: The script assumes a default ban time of 1 hour for calculating "Unban In". If your ban time is different, you can adjust this part of the script:

    ```bash
    time_left=$(( 3600 - (current_time - ban_time) ))
    ```

    Change `3600` to the appropriate number of seconds (e.g., for a 30-minute ban, use `1800`).

- **Update Interval**: The script refreshes every minute by default. If you want to change this, modify the `sleep` duration inside the `for i in {59..0}` loop.
