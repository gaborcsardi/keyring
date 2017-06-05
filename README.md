


# keyring

> Access the System Credential Store from R

[![Linux Build Status](https://travis-ci.org/gaborcsardi/keyring.svg?branch=master)](https://travis-ci.org/gaborcsardi/keyring)
[![Windows Build status](https://ci.appveyor.com/api/projects/status/github/gaborcsardi/keyring?svg=true)](https://ci.appveyor.com/project/gaborcsardi/keyring)
[![](https://www.r-pkg.org/badges/version/keyring)](https://www.r-pkg.org/pkg/keyring)
[![CRAN RStudio mirror downloads](https://cranlogs.r-pkg.org/badges/keyring)](https://www.r-pkg.org/pkg/keyring)
[![Coverage Status](https://img.shields.io/codecov/c/github/gaborcsardi/keyring/master.svg)](https://codecov.io/github/gaborcsardi/keyring?branch=master)

Platform independent API to access the operating systems
credential store. Currently supports:
* Keychain on macOS,
* Credential Store on Windows,
* the Secret Service API on Linux, and
* environment variables on all platforms.
Additional storage backends can be added easily.

## Installation

### Linux

Install the `libsecret` library, at least version 0.16.

- Debian/Ubuntu: `libsecret-1-dev`
- Recent RedHat, Fedora and CentOS systems: `libsecret-devel`

### OS X and Windows

No additional software needed

### R package


```r
source("https://install-github.me/gaborcsardi/keyring")
```

## Usage

### Configuring an OS-specific backend:

- The default is operating system specific, and is described in
  manual page of `default_backend()`. In most cases you don't have
  to configure this.
- MacOS: `backend_macos`
- Linux: `backend_secret_service`
- Windows: `backend_wincred`
- Or store the secrets in environment variables on other operating
  systems: `backend_env`

### Query secret keys in a keyring:

Each keyring can contain one or many secrets (keys). A key is defined by
a service name and a password. Once a key is defined, it persists in the
keyring store of the operating system. This means the keys persist beyond
the termination of and R session. Specifically, you can define a key
once, and then read the key value in completely independent R sessions.

- Setting a secret interactively: `key_set()`
- Setting a secret from a script, i.e. non-interactively:
  `key_set_with_value()`
- Reading a secret: `key_get()`
- Listing secrets: `key_list()`
- Deleting a secret: `key_delete()`

### Managing keyrings:

A keyring is a collection of keys that can be treated as a unit.
A keyring typically has a name and a password to unlock it.
See `keyring_create()`, `keyring_delete()`, `keyring_list()`,
`keyring_lock()`, `keyring_unlock()`, `keyring_is_locked()`.

Note that all platforms have a default keyring, and `key_get()`, etc.
will use that automatically. The default keyring is also convenient,
because the OS unlocks it automatically when you log in, so secrets
are available immediately.

You only need to explicitly deal with keyrings and the `keyring_*`
functions if you want to use a different keyring.

## Development documentation

Please see our [writeup of some `keyring` internals](https://github.com/gaborcsardi/keyring/blob/master/inst/development-notes.md),
and as always, use the source code.

## License

MIT © RStudio
