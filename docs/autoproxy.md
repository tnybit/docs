---
layout: default
title: Autoproxy
nav_order: 1
---

# Autoproxy
{: .no_toc }

Autoproxy is a tool that helps you automatically determines if you need a proxy (in a corporate environment), and then automatically setups your terminal/cli/cmd environment to use it.
{: .fs-6 .fw-300 }

[Visit the Github Repo](https://github.com/tnybit/autoproxy){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Getting Started

Autoproxy should be easy to install and start using. It's designed to help ease the pain of using proxy on the command line, especially when you don't have a choice, like when you're in a corporate environment.

### Homebrew

Installing via homebrew is pretty easy, just run:

```sh
brew install autoproxy
```

### Snapcraft

Snapcraft mainly focuses on linux based systems, but it also supports macOS.
Installing via snapcraft is also pretty easy, just run:

```sh
snap install autoproxy
```

### Source

Autoproxy is built in pure Rust, and is easy to build. Assuming you have a setup a valid toolchain, just run from the root of the project:

```sh
cargo build
```

If you wish to build and install it in one go, just run:

```sh
cargo install
```

## Running autoproxy

Whenever you need to set your `http(s)_proxy` variables, and assuming you have a good configuration, just run `autoproxy`. It will grab the config, test the connections available and determine if you need a proxy or not.

If you need a proxy, it will automatically set those variables in that shell session.

It's ideal to run this whenever you start a new shell session, so appending this command to your `.profile`, `.bashrc` or `.zshrc`.

## Enable and disable autoproxy

Sometimes you may wish to disable the autoproxy, and to do so you only need to run `autoproxy disable`. It will automatically `unset` the `http(s)_proxy` variables that it maintains. 

Once disabled though, you'll need to enable it manually by running `autoproxy enable`, or by directly modifying the config file.

## Adding a proxy

By default, the autoproxy is disabled until at least one proxy is added.
Adding a proxy is easy though, as you can do it with a single command:

```bash
autoproxy add \
--http "http://myproxy.com" \
--https "https://myproxy.com" \
--no "http://noproxy.com" \
myproxyname
```

If you need a deeper explaination, run `autoproxy add --help`

## Removing a proxy

Removing a proxy is easy, just run:

```bash
autoproxy remove myproxyname
```

## Postscripts

You can configure the application to execute a script whenever the `http(s)_proxy` variables are set and unset. It's ideal to use these scripts to set the proxy values for other applications that use a proxy, but though a opaque method.

For example, `npm` doesn't respect the `http(s)_proxy` values, but rather requires you to run something like:

```bash
# to set the value
npm config set proxy ${http_proxy}
npm config set https-proxy ${https_proxy}

# then to unset the value
npm config rm proxy
npm config rm https-proxy
```

So you can append those command into your respective postscripts, and autoproxy will run then whenever it sets or unsets the `http(s)_proxy` values.

## Config file

Autoproxy relies on a configuration file that sits in the user's filesystem.
It's a TOML file, and you can modify it however you like!

The location of the config file will vary depending on the operating system that it's running on.