#  :floppy_disk: ghbackup

[![GoDoc](https://godoc.org/qvl.io/ghbackup?status.svg)](https://godoc.org/qvl.io/ghbackup)
[![Build Status](https://travis-ci.org/qvl/ghbackup.svg?branch=master)](https://travis-ci.org/qvl/ghbackup)
[![Go Report Card](https://goreportcard.com/badge/qvl.io/ghbackup)](https://goreportcard.com/report/qvl.io/ghbackup)


    Embarrassing simple Github backup tool

    Usage: ghbackup [flags] directory

      directory  path to save the repositories to

    At least one of -account or -secret must be specified.

    Flags:
      -account string
            Github user or organization name to get repositories from.
            If not specified, all repositories the authenticated user has access to
    will be loaded.
      -secret string
            Authentication secret for Github API.
            Can use the users password or a personal access token (https://github.c
    om/settings/tokens).
            Authentication increases rate limiting (https://developer.github.com/v3
    /#rate-limiting) and enables backup of private repositories.
      -verbose
            print progress information

    For more visit https://qvl.io/ghbackup.


The simplest way to keep your repositories save:

1. [Install](#install) `ghbackup`
1. Get a token from https://github.com/settings/tokens
2. `ghbackup -secret token /path/to/backup/dir`

This will backup all repositories you have access to.


## Install

- With [Go](https://golang.org/):
```
go get qvl.io/ghbackup
```

- With [Homebrew](http://brew.sh/):
```
brew install qvl/tap/ghbackup
```

- Download binary: https://github.com/qvl/ghbackup/releases


## Automation

Mostly, we like to setup backups to run automatically in an interval.
There are different tools to do this:

### Cron

Cron is a job scheduler that already runs on most Unix systems.

Let's setup `ghbackup` on a Linux server and make it run daily at 1am. This works similar on other platforms.

1. Install `ghbackup`: `go get qvl.io/ghbackup`

2. Setup Cron job

- Run `crontab -e`
- Add a new line and replace `NAME` and `DIR` with your options:

``` sh
0 1 * * * ghbackup -account NAME DIR
```

For example:

``` sh
0 1 * * * ghbackup -account qvl /home/qvl/backup-qvl
```


## What happens?

Get all repositories of a Github account.
Save them to a folder.
Update already cloned repositories.

Best served as a scheduled job to keep your backups up to date!


## Limits

`ghbackup` is about repositories.
There are other solutions if you like to backup issues and wikis.


## Use as Go package

From another Go program you can directly use the `ghbackup` sub-package.
Have a look at the [GoDoc](https://godoc.org/qvl.io/ghbackup/ghbackup).


## Development

Make sure to use `gofmt` and create a [Pull Request](https://github.com/qvl/ghbackup/pulls).

### Releasing

Push a new Git tag and [GoReleaser](https://github.com/goreleaser/releaser) will automatically create a release.


## License

[MIT](./license)
