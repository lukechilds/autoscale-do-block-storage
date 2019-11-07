# checkvolumesize

> Autoscale Digital Ocean block storage volumes

Create a Digital Ocean block storage volume and write as much data to it as you want. Run this script on cron to monitor the volume and automatically scale it up in size as required with zero downtime.

Don't worry about manually resizing or running out of space and save money by only paying for what you use.

Inspired by this feature request:
- https://twitter.com/lukechilds/status/1192252814262599680
- https://ideas.digitalocean.com/ideas/BSX-I-6

## Usage

```
$ checkvolumesize --help
checkvolumesize 1.0.0

Automatically expand Digital Ocean block storage volumes.

Usage: checkvolumesize [options]

Options:

  --help | -h | help    [Optional] Show this help message
  --token               [Required] Digital Ocean API token
  --device              [Required] The volume's block device
  --volume-name         [Required] The volume's name
  --volume-region       [Required] The volume's region
  --buffer              [Optional] The amount of GB to keep available    Default: 10
  --log                 [Optional] Prepend timestamps to stdout

Example:

  checkvolumesize /
    --token bc99be9f73b037da64074472fe58f643e619328b85c5467615964a59abd12029 /
    --device /dev/sda /
    --volume-name volume-sgp1-01 /
    --volume-region sgp1 /
    --buffer 10

GitHub: https://github.com/lukechilds/autoscale-do-block-storage
```

## Demo

```
$ checkvolumesize --token bc99be9f73b037da64074472fe58f643e619328b85c5467615964a59abd12029 --device /dev/sda --volume-name volume-sgp1-01 --volume-region sgp1 --buffer 10
Checking available space on device "/dev/sda" is above 10GB requirement...
Only 8GB available, volume resize required
Getting data for volume "volume-sgp1-01" in region "sgp1"...
Volume ID is "2cbebc6a-ff42-11e9-a238-0a58ac14a19d" and is currently 430GB
Increasing volume size to 440GB...
Created action "796611989"
Waiting for action to complete...
Volume resize complete!
Resizing filesystem...
resize2fs 1.44.1 (24-Mar-2018)
Filesystem at /dev/sda is mounted on /mnt/volume_sgp1_01; on-line resizing required
old_desc_blocks = 54, new_desc_blocks = 55
The filesystem on /dev/sda is now 115343360 (4k) blocks long.
Filesystem resize complete!
Device "/dev/sda" now has 17GB available
Completed in 16 seconds
```

## License

MIT © Luke Childs
