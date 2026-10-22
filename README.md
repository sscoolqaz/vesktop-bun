# vesktop-bun

AUR package for [Vesktop](https://github.com/Vencord/Vesktop) built from the
release source with [bun](https://bun.sh) instead of pnpm.

It installs to the same paths as `vesktop` / `vesktop-bin` (`/usr/lib/vesktop`,
launcher `vesktop`), so it provides `vesktop` and conflicts with both.

## Install

```sh
yay -S vesktop-bun   # or any AUR helper
```

Extra launch flags go in `~/.config/vesktop-flags.conf`, one per line (a line
is passed as one argument, spaces included; lines starting with `#` are skipped).

## Building

The PKGBUILD is based on the AUR `vesktop` package. Differences:

- Upstream's `pnpm-lock.yaml` is migrated to `bun.lock` with `bun pm migrate`,
  so the build uses the same pinned dependency versions as upstream.
- The `link:packages/libvesktop` dependency is dropped before migrating (bun
  can't migrate relative links). bun still compiles libvesktop from source as
  a workspace with node-gyp, so the app uses that build instead of the
  upstream prebuilt binary.
- Dependencies are installed with `--linker hoisted`, matching upstream's pnpm
  `nodeLinker: hoisted`.

## Links

- Upstream: https://github.com/Vencord/Vesktop
- AUR: https://aur.archlinux.org/packages/vesktop-bun
