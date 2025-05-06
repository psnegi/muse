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
- **immich-go** -server=http://SERVER_IP:PORT -key=XXXXAPIKEYGOESHEREXXXXXXXX upload -dry-run -create-albums -google-photos takeout-*.zip         
