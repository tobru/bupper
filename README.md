# bupper - a bup backup profile manager

## Introduction

bupper is a profile manager for [bup](https://github.com/bup/bup), the backup utility based on git. It helps you to create backup profiles with pre- and post-backup tasks, excludes, backup destinations and much more.

## Installation

* Install [bup](https://github.com/bup/bup) > 0.25
* `gem install bupper`

## Configuration

The configuration is done in `/etc/bupper.yml` or in the config file you specify with `--config <filename>`.

``` yaml
---
global:
  log_dir: '/var/log/bupper'
profile1:
  source: '/'
  destination: ''
  remote: false
  mail_recipient: 'admin@mydomain.tld'
  pre_backup_command: ''
  post_backup_command: ''
  pre_restore_command: ''
  post_restore_command: ''
  backup_exclude:
    - 'dir1'
    - 'dir2'
```

## Usage

### Backup

* `bupper backup <profilename>`
* `bupper backup all`

### Restore

* `bupper restore init <name>`
* `bupper restore init all`
* `bupper restore finish <name>`
* `bupper restore finish all`

### Other

* `bupper help`

### Parameter

* `--config`: Path to the config file (Default: `/etc/bupper.yml`

### Notes

## License

tbd

## Addendum

This project was done by following the [Readme Driven Development](http://tom.preston-werner.com/2010/08/23/readme-driven-development.html) pattern.
