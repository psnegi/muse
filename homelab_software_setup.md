# Homelab setup
- Setup RPI with external SSD. Following this setup of [RPI with external SSD][https://raspibolt.org/]
- Follow [link](https://diycraic.com/2024/08/17/raspberry-pi-home-server-tutorial/) for docker setup and docker management tool portainer and duplicati(backup) and basic home page setup
- Follow [link](https://immich.app/docs/install/portainer/) for immich in portianer setp

# Google take of photos
Assumes you have immich setup and running
- Install [immich-go](https://github.com/simulot/immich-go)
  - Make sure you have go and git intstalled.
    - [go install](https://go.dev/doc/install)
- [google take out][ https://takeout.google.com]. Deselect all, select only photos, select dowload type and size
- Download the take* file in folder. key in following command can be created from immich setting.
- Do dry run -dry-run and if output looks ok run without it 
- **immich-go** immich-go upload from-google-photos --server=http://server:port --api-key=.... --dry-run  takeo*.zip
# Setting up home assistant

## wifif setup
- Isntall shh from setting, addon and  search ssh
- ha  network update wlan0 --ipv4-method auto --ipv6-method auto --wifi-auth wpa-psk --wifi-mode infrastructure --wifi-ssid "YOUR_SSID" --wifi-psk "YOUR_WIFI_PASSWORD"
