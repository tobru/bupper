# bupper - a bup backup profile manager

## Introduction

bupper is a profile manager for [bup](https://github.com/bup/bup), the backup utility based on git. It helps you to create backup profiles with pre- and post-backup tasks, excludes, backup destinations and much more.

## Installation

* Install [bup](https://github.com/bup/bup) > 0.25
  Ubuntu 14.04 has already this version shipped: `apt-get install bup`
* Optional: Install `sshfs`, needed for restoring from remote server
* `gem install bupper`

## Configuration

The configuration is done in `/etc/bupper.yml` or in the config file you specify with `--config <filename>`. Example:

``` yaml
---
global:
  log_dir: '/var/log/bupper'
  log_level: 'debug'
profiles:
  profile_local:
    source:
      - '/etc'
    bup_dir: '/var/lib/backup/bup'
    pre_backup_commands:
      - '/usr/local/bin/pre_backup.sh'
    post_backup_commands:
      - '/usr/local/bin/post_backup.sh'
    backup_exclude:
      - 'passwd'
      - 'shadow'
  profile_remote:
    source: '/tmp'
    remote: true
    destination: 'server:/var/lib/backup'
```

## Usage

To use bup, you need to initialize a local repository: `bup init`.
If you're using `bup_dir` in the configuration file to specify the working directory, use `BUP_DIR=<dir> bup init`
The default for `bup_dir` is `/root/.bup`

### Backup

* `bupper backup -p <profilename>`
* `bupper backup -p all`

### Restore

* `bupper restore -a init -p <name>`
* `bupper restore -a init -p all`
* `bupper restore -a finish -p <name>`
* `bupper restore -a finish -p all`

### Other

* `bupper -h`: help

### Parameter

* `-c | --config`: Path to the config file (Default: `/etc/bupper.yml`
* `-p | --profile`: Name of the profile or `all` (Default: all)

### Notes

* Restore is not yet implemented, you have to mount sshfs by yourself
* The GEM is not available yet as it's just not done

### TODO

* Make a GEM
* Cleanup all ugly Ruby things which I did wrong
* Move functions into lib

## License

tbd

## Addendum

This project was done by following the [Readme Driven Development](http://tom.preston-werner.com/2010/08/23/readme-driven-development.html) pattern.
It's my first Ruby project, so bear with me for the ugliness.
