Pre-requisites
=======

```
apt-get install build-essential libssl-dev libcurl4-openssl-dev pkg-config libssh2-1-dev
```

Rust compiler from trusted build roots
======

This repository aims to build the Rust compiler without using the Rust compiler binary.

http://vxer.org/lib/pdf/Reflections%20on%20Trusting%20Trust.pdf

HOWTO
======

The following was tested on Debian 9.  Total build time is 2-3 hours because of lack
of parallelism in the rustc bootstrap phase.

```
sudo apt install build-essential cmake curl git diffoscope
./go-fetch

# from this point on, there should be no network access
./go-build
./go-compare
```

diffoscope result will be in `report.md` and various logs in `*.log`.

TODO
======

- Better vendoring of sources
- Ensure no unexpected network access by build scripts
- Evaluate artifacts other than `rustc`

