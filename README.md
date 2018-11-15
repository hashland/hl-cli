```
   _                  _      _                    _ 
  | |                | |    | |                  | |
  | |__    __ _  ___ | |__  | |  __ _  _ __    __| |
  | '_ \  / _` |/ __|| '_ \ | | / _` || '_ \  / _` |
  | | | || (_| |\__ \| | | || || (_| || | | || (_| |
  |_| |_| \__,_||___/|_| |_||_| \__,_||_| |_| \__,_|
  
           Hashland Command Line Interface
```

## Usage

```
$ hl ethers|miners|miner_types|sensors|temp [param=value]
```

## Examples

```
List miners by name:
$ hl miners name=XXX

List miners by mac:
$ hl miners mac=02:42:0d:f2:39:6a

List miners by miner_type:
$ hl miners miner_type=1b45a531-93e7-11e8-bd87-02420a000145

List all miner types:
$ hl miner_types

List all sensors:
$ hl sensors

Get all temperature sensors:
$ hl temp
```
