# Google take of photos
Assumes you have immich setup and running
- Install [immich-go](https://github.com/simulot/immich-go)
  - make sure you have  go and git intstalled.
    - [go install](https://go.dev/doc/install)
- [google take out][ https://takeout.google.com]. Deselect all, select only photos, select dowload type and size
- Download the take* file in folder. key in following command can be created from immich setting.
- Do dry run -dry-run and if output looks ok run without it 
- immich-go -server=http://SERVER_IP:PORT -key=XXXXAPIKEYGOESHEREXXXXXXXX upload -dry-run -create-albums -google-photos takeout-*.zip         
