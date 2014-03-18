# bupper - a bup backup profile manager

## Introduction

bupper is a profile manager for [bup](https://github.com/bup/bup), the backup utility based on git. It helps you to create backup profiles with pre- and post-backup tasks, excludes, backup destinations and much more.

## Installation

`gem install bupper`

## Configuration

The configuration is done in `/etc/bupper.yml` or in the config file you specify with `--config <filename>`.

``` yaml
---
global:
  log_dir: '/var/log/bupper'
```

## Usage
