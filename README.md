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

```
# Generate /etc/ethers file:
$ hl ethers

# List miners json by name:
$ hl miners name=XXX

# List miners json by mac:
$ hl miners mac=02:42:0d:f2:39:6a

# List miners json by miner_type:
$ hl miners miner_type=1b45a531-93e7-11e8-bd87-02420a000145

# Export miners to csv file:
$ hl miners | jq -r '[.name, .ip, .mac] | @csv' >export.csv

# List all miner types json:
$ hl miner_types

# List all sensors json:
$ hl sensors

# Get all temperature sensors and their current values:
$ hl temp
```
