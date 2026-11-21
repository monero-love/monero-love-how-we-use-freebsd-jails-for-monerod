# How We Use FreeBSD Jails for monerod: configuration examples

Source: https://monero.love/guides/how-we-use-freebsd-jails-for-monerod/

These are the published FreeBSD settings. The package repository file belongs inside the jail at `/usr/local/etc/pkg/repos/monero-love.conf`. Independently verify the repository signing key and install it at `/usr/local/etc/pkg/keys/monero-love.pub` before using pkg. The article describes the unofficial `monerod-love` package and its `monerod_love` service.

Merge `jail/rc.conf.fragment` into the jail's rc.conf only after configuring the packaged daemon. The package supplies its daemon configuration and service script. This repository does not invent a Bastille jail definition or overwrite those defaults.

The PF and sysctl fragments belong on the FreeBSD host, not inside the jail. Replace `ix0` and `10.170.100.10` with your actual interface and assigned jail address. The jail and its networking must already exist. Merge PF macros, options, translation and filter rules into the corresponding sections of your existing ruleset, preserving management access and its default policy. This fragment is not a complete firewall. It exposes only P2P port 18080, not wallet RPC.

Review capacity before changing limits. Do not lower larger existing limits merely to match the example. Run `pfctl -nf /etc/pf.conf` on the assembled configuration before loading it. Check process descriptor limits after the normal service restart.

References: [FreeBSD jails](https://docs.freebsd.org/en/books/handbook/jails/), [pf.conf](https://man.freebsd.org/cgi/man.cgi?query=pf.conf&sektion=5).

## Files

- `pkg/monero-love.conf`
- `host/pf.fragment.conf`
- `host/sysctl.fragment.conf`
- `jail/rc.conf.fragment`

`ARTICLE-EXAMPLES.md` preserves the published code blocks for context. It is a reference, not a script to execute in one pass. `SOURCE.json` identifies the fetched page and packaged file hashes. No services were installed or restarted when preparing this repository.
