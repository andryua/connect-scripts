# Update sync.conf

This folder contains set of scripts and components necesssary to change your Agent's sync.conf file via Distribution job. Script also restarts agent service if necesary. The script does not care about the folder it runs into.
Minimal set of files that should be present in distribution folder
* update-syncconf.ps1

The files *.copy_to_trigger are not necessary to be present in distributed folder but copied to the trigger of update job on MC. 

## update-syncconf.ps1 ![alt text](https://i.imgur.com/F6NAQyb.png "Script supports standard Get-Help cmdlet")
The script is actually doing an update of sync.conf, which includes:
* loading existing sync.conf from standard or specified location
* modifying sync.conf according to specified parameters
* saving sync.conf into the same location
* restarting the agent if requested
* restarting the agent via detached way (using Windows Task Scheduler) if requested

## ResilioRestart.xml
This XML spawned automatically into a target folder by script if agent restart is requested

## upgrade-post-download.cmd.copy_to_trigger
This file contains cmd script which needs to be placed to post-download trigger of the update job. Please note that you need to specify necessary parameterys yourself before firing the job

## update-syncconf.py
Script for Mac OS.
Do the same things as update-syncconf.ps1, excepting agent restart

$ ./update-syncconf.py --help
usage: update-syncconf.py [-h] [--conf <path_to_sync.conf>]
                          [--parameter <name>] [--value <value>]
                          [--delete <parameter_name>] [--host <value>]
                          [--fingerprint <value>]
                          [--disable_cert_check <value>]
                          [--bootstrap_token <value>] [--tags <value>]
                          [--folders_storage_path <value>]

optional arguments:
  -h, --help            show this help message and exit
  --conf <path_to_sync.conf>
                        path to sync.conf (default:
                        /Users/<username>/Library/Application Support/Resilio Connect
                        Agent/sync.conf)
  --parameter <name>    name of parameter to manipulate
  --value <value>       value to set to parameter
  --delete <parameter_name>
                        delete parameter
  --host <value>        value to set to host
  --fingerprint <value>
                        value to set to fingerprint
  --disable_cert_check <value>
                        value to set to disable_cert_check
  --bootstrap_token <value>
                        value to set to bootstrap_token
  --tags <value>        value to set to tags
  --folders_storage_path <value>
                        value to set to folders_storage_path