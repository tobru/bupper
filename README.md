# bupper - a bup backup profile manager

## Introduction

bupper is a profile manager for [bup](https://github.com/bup/bup), the backup utility based on git. It helps you to create backup profiles with pre- and post-backup tasks, excludes, backup destinations and much more.

## Installation

* Install [bup](https://github.com/bup/bup) > 0.25
  Ubuntu 14.04 has already this version shipped: `apt-get install bup`
* Optional: Install `sshfs`, needed for restoring from remote server
* `git clone https://github.com/tobru/bupper.git && cd bupper && ln -s $(pwd)/bin/bupper /usr/local/bin/bupper`

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

### Detailed configuration parameter description

**global**

* *log_dir* (string): path where the log will be saved
* *log_level* (string): choose one of: debug, info, warn, error, fatal, unknown

**profiles**

The profile name should only contain letters and underscores.

* *source* (array): source directories for the backup
* *bup_dir* (string): bup working directory, defaults to /root/.bup
* *remote* (boolean): is the destination local or remote
* *destination* (string): destination for remote backups
* *backup_exclude* (array): exclude directories or files
* *pre_backup_commands* (array): commands to execute before the backup
* *post_backup_commands* (array): commands to execute after the backup

## Usage

To use bup, you need to initialize a local repository: `bup init`.
If you're using `bup_dir` in the configuration file to specify the working directory, use `BUP_DIR=<dir> bup init`
The default for `bup_dir` is `/root/.bup`

### Backup

This runs `bup index` and `bup save` and the specified pre- and post-backup scripts (if there are any)

* `bupper backup -p <profilename>`
* `bupper backup -p all`

### Restore

It just outputs some help text, but does nothing by itself.

* `bupper restore -p <profilename>`
* `bupper restore -p all`

### Other

* `bupper -h`: help

### Parameter

* `-c | --config`: Path to the config file (Default: `/etc/bupper.yml`
* `-p | --profile`: Name of the profile or `all` (Default: all)

## The MIT License (MIT)

```
Copyright (c) 2014 Tobias BRunner

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## Addendum

This project was done by following the [Readme Driven Development](http://tom.preston-werner.com/2010/08/23/readme-driven-development.html) pattern.
It's my first Ruby project, so bear with me for the ugliness.
