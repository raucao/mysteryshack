# mysteryshack [![Build Status](https://travis-ci.org/untitaker/mysteryshack.svg?branch=master)](https://travis-ci.org/untitaker/mysteryshack)

<img src="https://shack.unterwaditzer.net/static/logo.svg" width=120 height=120 />

Mysteryshack is a lightweight, yet self-contained
[remoteStorage](http://remotestorage.io/)-server.

***This project is still in active development. Do not use with sensitive data, or without backup.***

Use username `demo` and password `demo` on [my
server](https://shack.unterwaditzer.net) to try it out.

## Installation

### Using precompiled binary

Download [the precompiled binary](https://unterwaditzer.net/bin/mysteryshack),
and stick it somewhere into your PATH.

The binary has been compiled on CentOS 6.7. It seems to work correctly on other
RedHat distributions. If you're on some other system, you probably have to
either build your own or set some symlinks.

### Building own binary

* Install [Rust](https://www.rust-lang.org/).
* Clone this repository.
* Run `cargo build --release`.
* Stick `./target/release/mysteryshack` into your PATH.

## Usage

* Unfortunately for now you still need to `cd` into the repository's root, so
  that mysteryshack can find its favicon, css etc. [See the relevant
  issue](https://github.com/untitaker/mysteryshack/issues/8).
* Edit `config.example` and save it as `config`.
* `mysteryshack user create foo` to create a new user. See also `mysteryshack
  --help` and `mysteryshack user --help`.
* `mysteryshack serve` to run the server as configured in `./config`.

## Troubleshooting

### OS X and OpenSSL

As of OS X 10.11, OpenSSL isn't installed anymore. You'll need to install it manually:

    brew install openssl
    brew link --force openssl

## Implementation notes

* Mysteryshack implements `draft-dejong-remotestorage-05.txt`, however, it
  sends two kinds of webfinger responses to stay compatible with
  `remotestorage.js`.

* Mysteryshack is set up to be tested against the official [api test
  suite](https://github.com/remotestorage/api-test-suite/) automatically (in
  Travis).

* Mysteryshack's approach to concurrency is very simplistic, but is certainly
  enough for smaller to medium-sized servers.

* Mysteryshack stores OAuth tokens on the harddrive, but web admin sessions are
  stored inside signed cookies. The key is generated at server startup. To log
  everybody out, restart the server.

## License

* Logo is licensed under
  [CC-BY-SA](https://creativecommons.org/licenses/by-sa/3.0/), based on:

  * [Rust logo, CC-BY](https://www.rust-lang.org/legal.html)

  * [remoteStorage logo, CC-BY-SA](https://github.com/remotestorage/design)

* Source code is licensed under the MIT, see `LICENSE`.
