# lcd4linux-docker

1. Attach Display
2. Find the right Port for the Display, my Alphacool has VENDOR-ID: 060c and Device-ID: 04eb
   ```
   $ lsusb |grep 060c:04eb
   Bus 001 Device 006: ID 060c:04eb EEH Datalink GmbH ALPHACOOL USB DISPLAY
   ```
3. So, the right Path for docker-compose.yml should be
   `/dev/bus/usb/001/006`
   ```
    services:
      lcd4linux:
        build: .
        image: djusha/lcd4linux:latest
        container_name: lcd4linux
        restart: always
        volumes:
          - ./lcd4linux/lcd4linux.conf:/etc/lcd4linux.conf
        devices:
          - /dev/bus/usb/001/006:/dev/bus/usb/001/006
   ```
4. Edit `lcd4linux.conf`
5. Start Container `docker-compose up -d`

[LCD4Linux Wiki](https://wiki.lcd4linux.tk/doku.php)
