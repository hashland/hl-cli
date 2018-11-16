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
usage: hl dlsysimage|ethers|miners|miner_types|pdus|pdu_types|ping_miners|racks|sensors|set_miner|ssh_miners|sysimage|sysimages|temp [param=value]
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

# All miners with type
$ hl miners miner_type=1b45a531-93e7-11e8-bd87-02420a000145

# All miners in rack
$ hl miners rack=17621f2a-93e8-11e8-bd87-02420a000145

# All miners with type in rack
$ hl miners "rack=17621f2a-93e8-11e8-bd87-02420a000145&miner_type=1b45a531-93e7-11e8-bd87-02420a000145"

# you can also specify an array in the filters, e.g. get all miners from rack a and b (note the quotes because of the &)
$ hl miners "rack[]=171fd01d-93e8-11e8-bd87-02420a000145&rack[]=172645e3-93e8-11e8-bd87-02420a000145"
```

#### run ssh command on a miner set

```
# run ssh command on all miners from the specified racks

$ hl ssh_miners "rack[]=171fd01d-93e8-11e8-bd87-02420a000145&rack[]=172645e3-93e8-11e8-bd87-02420a000145" uptime

```

#### ping miners
```
# ping all miners
$ hl ping_miners

# ping all miners for filter
$ hl ping_miners "rack[]=171fd01d-93e8-11e8-bd87-02420a000145&rack[]=172645e3-93e8-11e8-bd87-02420a000145" 

```

#### set parameters for a miner
```
# set mac address for a given miner
$ hl set_miner 1770c711-93e8-11e8-bd87-02420a000145 mac=02:42:07:93:53:B7
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

### Racks

#### List all racks:
```
$ hl racks
{
  "id": "17621f2a-93e8-11e8-bd87-02420a000145",
  "created_at": 1532948566,
  "name": "DD.F"
}
...
```


### Power Distribution Units (PDUs)

#### List all pdus:
```
$ hl pdus

{
  "id": "167f227c-93e8-11e8-bd87-02420a000145",
  "created_at": 1532948565,
  "updated_at": 1542358804,
  "name": "RPC3A7",
  "pdu_type": {
    "id": "0ab36207-93e7-11e8-bd87-02420a000145",
    "name": "RPC-3A",
    "vendor": "BayTech",
...
```

### Power Distribution Unit Types

#### List all pdu types:
```
$ hl pdu_types

{
  "id": "0ab36207-93e7-11e8-bd87-02420a000145",
  "name": "RPC-3A",
  "vendor": "BayTech",
  "slots": 8,
  "ampere": 10
}
...

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

```
$ hl ethers

02:42:EA:81:E2:9A 10.2.1.84
02:42:B7:8A:EE:17 10.2.1.85
02:42:8B:A2:2A:5A 10.2.1.86
...
```
