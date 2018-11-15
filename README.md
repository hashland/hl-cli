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
$ hl ethers|miners|miner_types|sensors|temp [param=value]
```

## Examples

### Miners

#### List all miners:
```
$ hl miners
```

#### List miners with filter:
```
$ hl miners mac=02:42:0d:f2:39:6a

$ hl miners name=XXX

$ hl miners miner_type=1b45a531-93e7-11e8-bd87-02420a000145
```

#### Export miners to csv file:
```
$ hl miners | jq -r '[.name, .ip, .mac] | @csv' >export.csv
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
{
  "id": "896d14b5-0a9d-4a95-a256-737b2bcd1242",
  "created_at": 1542202321,
  "name": "baikal,giant-b",
  "url": "http://cdn.hashland.cc/hlos/18.11-beta3/targets/sunxi/cortexa7/hashland-18.11-beta3-sunxi-cortexa7-baikal-giant-b-squashfs-sdcard.img",
  "version": "18.11-beta3"
}
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

```
# Generate /etc/ethers file:
$ hl ethers

# List all miner types json:
$ hl miner_types

# List all sensors json:
$ hl sensors

# Get all temperature sensors and their current values:
$ hl temp
```
