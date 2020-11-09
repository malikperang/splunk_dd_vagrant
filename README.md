## Requirements

- Vagrant 2.2 or above.
- VirtualBox 6.1 or above.

## Server Specs
``` 
searchead1 
Operating System: Centos 7 
CPU Core: 2 Memory: 2GB 
Private IP Address: 192.168.20.21 

indexer01 
Operating System: Centos 7 
CPU Core: 2 
Memory: 2GB 
Private IP Address: 192.168.20.22 

indexer02 
Operating System: Centos 7 
CPU Core: 2 
Memory: 2GB 
Private IP Address: 192.168.20.23 

forwarder01 
Operating System: Centos 7 
CPU Core: 2 
Memory: 2GB 
Private IP Address: 192.168.20.24 
```

## Installation

Bring up the servers

```
$ vagrant up
```

if prompted for machine password, please specify since it will alter `Host` file in local machine.

The initial setup will do the Splunk Enterprise installation automatically.
It will install Splunk on `/opt/splunk` directory on each servers.

After initial setup is completed, login to each instance to start the Splunk Enterprise 
instance and accept the license as well as adding admin user for each Splunk Enterpriese instance.

#### Example for Search Head

Login to searchead1
```
$ vagrant ssh searchead1
```

Start Splunk and accept the license. 
```
$ splunk start --accept-license
```
It will prompt for administrator `username` and `password`, please fill-in this accordingly.

Please repeat the same process for other instances.

## Verify Installation

Visit Search Head Splunk Web at `http://192.168.20.21:8000`. 
You will see Splunk Web authentication page if you follow the correct steps.

Please repeat the same process for other instances.

Thank you

by [Fariz Izwan @ Malik Perang](https://github.com/malikperang)
