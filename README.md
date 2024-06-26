# Gemserv

A gemini server written in rust.

## Features

 - Vhosts
 - CGI
 - User directories
 - Reverse proxy
 - Redirect
 - SCGI
 - Reload config on SIGHUP

## Installation and running

To run either run "cargo run /path/to/config" or if no configuration is
specified it will look for "/usr/local/etc/gemserv.conf"

### Prebuilt binaries

You can download prebuilt binaries for linux on the release page.

### Install from crates.io:

cargo install gemserv

### Install from docker

docker pull 080h/gemserv

### Build from source:

 - Clone the repo
 - If you want to use all features run 'cargo build --release' or if you only
   want to serve static files run 'cargo build --release --no-default-features'
 - Modify the config.toml to your needs
 - Run './target/release/gemserv config.toml'

## Init scripts

In the init-scripts directory there's OpenRC(Courtesy of Tastytea) and systemd
service files.

## CGI and SCGI

There's example SCGI scripts for python and perl in the cgi-scripts directory.

In the configuration file there's "cgi" which is an optional bool to turn cgi
on. If it's true it'll run scripts from any directory. To limit it to only one
directory set "cgipath"

If "cgi" is false or not set the server will respond "Not Found" to any
executable file.

Scripts have 5 seconds to complete or they will be terminated.

### CGI Environments

These variables are preset for you. If you need more you can define them in the
config file under "cgienv"

 - GEMINI_URL
 - SERVER_NAME
 - SERVER_PROTOCOL
 - SERVER_SOFTWARE
 - SCRIPT_NAME
 - REMOTE_ADDR
 - REMOTE_HOST
 - REMOTE_PORT
 - QUERY_STRING
 - PATH_INFO

TLS variables
 - AUTH_TYPE
 - TLS_CLIENT_HASH
 - REMOTE_USER

## Changelog

### [0.6.6] - 20220217

Bug fix: File path is checked to make sure it's in the root directory or in ~/public_gemini

### [0.6.5] - 20220209

Bug fix: Another traversal bug.

### [0.6.4] - 20220202

Fixed a file system traversal bug. All previous versions are unsafe.
