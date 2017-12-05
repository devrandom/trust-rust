Rust compiler from trusted build roots
======

This repository aims to build the Rust compiler without using the Rust compiler binary.

http://vxer.org/lib/pdf/Reflections%20on%20Trusting%20Trust.pdf

HOWTO
======

The following was tested on Debian 9.  Total build time is 2-3 hours because of lack
of parallelism in the rustc bootstrap phase.

```
sudo apt install build-essential cmake curl git diffoscope libssl-dev libcurl4-openssl-dev pkg-config libssh2-1-dev
./go-fetch

# from this point on, there should be no network access
./go-build
./go-compare
```

diffoscope result will be in `report.md` and various logs in `*.log`.

USE
======

After building, do the following:

```
mkdir trusted
cp -a trust-rust/stage0/bin trusted
cp -a trust-rust/rust/build/x86_64-unknown-linux-gnu/stage2/* trusted
PATH=`pwd`/trusted/bin:$PATH
```

`rustc -V` should produce `rustc 1.19.0-dev (0ade33941 2017-07-17)`.

TODO
======

- cargo TLS
- Evaluate artifacts other than `rustc` with diffoscope
- Check how far we are from a deterministic build

