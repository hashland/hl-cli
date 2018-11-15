```
   _                  _      _                    _ 
  | |                | |    | |                  | |
  | |__    __ _  ___ | |__  | |  __ _  _ __    __| |
  | '_ \  / _` |/ __|| '_ \ | | / _` || '_ \  / _` |
  | | | || (_| |\__ \| | | || || (_| || | | || (_| |
  |_| |_| \__,_||___/|_| |_||_| \__,_||_| |_| \__,_|
  
           Hashland Command Line Interface
```

## Dependencies
* `curl`
* `jq` Install it with `apt install jq` on Debian/Ubuntu and `brew install jq` on OSX

## API Key
Create a file in your home directory containing the api key with `echo API_KEY=xxxyourxxxapixxxkeyxxx >$HOME/.hashland && chmod 600 $HOME/.hashland`
## Usage

```
usage: hl dlsysimage|ethers|miners|miner_types|sensors|sysimage|sysimages|temp [param=value]
```

## Examples

### Miners

#### List all miners
```
$ hl miners
{
  "id": "1466f77b-93e8-11e8-bd87-02420a000145",
  "created_at": 1532948561,
  "updated_at": 1542095106,
  "name": "ANTD3002",
  "rack_position": "37R",
  "ip": "10.3.1.2",
  "mac": "90:70:65:B7:C4:05",
  "active": true,
...
```

#### List miners with filter
```
$ hl miners mac=02:42:0d:f2:39:6a

$ hl miners name=XXX

$ hl miners miner_type=1b45a531-93e7-11e8-bd87-02420a000145
```

#### Export miners to csv file
```
$ hl miners | jq -r '[.name, .ip, .mac] | @csv' >export.csv
```

### Miner Types

#### List all miner types
```
$ hl miner_types
{
  "id": "2d291c57-bfef-4b5b-a24f-9d5d3d335caa",
  "name": "BK-G28",
  "manufacturer": "Baikal",
  "algorithms": {
    "x11": {
      "kw": "1.3",
      "hashrate": "28 GH/s"
    },
    ...
```

### Hashland OS System Images

#### List all available Hashland OS System Images
```
$ hl sysimages
{
  "id": "408b154f-e8f1-11e8-b7fa-02420a000150",
  "created_at": 1542298350,
  "name": "baikal,giant-b",
  "url": "http://cdn.hashland.cc/hlos/18.11-beta4/targets/sunxi/cortexa7/hashland-18.11-beta4-sunxi-cortexa7-baikal-giant-b-squashfs-sdcard.img",
  "version": "18.11-beta4"
}
...
```

#### List best version for specific board / version

Get latest version with `beta` stability for `baikal,giant-b`:

```
$ hl sysimage baikal,giant-b @beta  
{
  "id": "408b154f-e8f1-11e8-b7fa-02420a000150",
  "created_at": 1542298350,
  "name": "baikal,giant-b",
  "url": "http://cdn.hashland.cc/hlos/18.11-beta4/targets/sunxi/cortexa7/hashland-18.11-beta4-sunxi-cortexa7-baikal-giant-b-squashfs-sdcard.img",
  "version": "18.11-beta4"
}
```

Get latest version with `stable` stability for `baikal,giant-b`:

```
$ hl sysimage baikal,giant-b @stable  
{
  "id": "408b154f-e8f1-11e8-b7fa-02420a000150",
  "created_at": 1542298350,
  "name": "baikal,giant-b",
  "url": "http://cdn.hashland.cc/hlos/18.11/targets/sunxi/cortexa7/hashland-18.11-sunxi-cortexa7-baikal-giant-b-squashfs-sdcard.img",
  "version": "18.11"
}
```
### Download best version for specific board / version
```
$ hl dlsysimage baikal,giant-b @beta
Downloading hashland-18.11-beta4-sunxi-cortexa7-baikal-giant-b-squashfs-sdcard.img
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 14.9M  100 14.9M    0     0  5504k      0  0:00:02  0:00:02 --:--:-- 5629k
```

### Sensors

#### List all sensors and their values
```
# List all sensors json:
$ hl sensors
{
  "id": "7152eb3f-a6e2-11e8-8baf-02420a0001a5",
  "created_at": 1535035212,
  "updated_at": 1542317461,
  "name": "Rack",
  "type": "DH18S20",
...
```

#### Get values from all temperature sensors
```
$ hl temp
Außentemperatur: 6.1
Büro: 18.9
Gang Regale: 33.6
...
```
### Generate /etc/ethers file

ethers - Ethernet address to IP number database. Can be used by DHCP server to assign static ip leases.

$ hl ethers
02:42:EA:81:E2:9A 10.2.1.84
02:42:B7:8A:EE:17 10.2.1.85
02:42:8B:A2:2A:5A 10.2.1.86
...
