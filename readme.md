[deploy-rs]: https://github.com/serokell/deploy-rs
[github-workflow]: https://github.com/mibmo/deployrs-binary-cache/actions/workflows/populate-cache.yaml

# !! NO LONGER MAINTAINED !! MOVED TO [cache-it](https://github.com/mibmo/cache-it)
The cache (deploy-rs.cachix.org) is still actively populated and with the same keys, but the code for doing so is no longer located here.

---
---
---
---
---

# Binary cache for [deploy-rs][deploy-rs]
[![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/mibmo/deployrs-binary-cache/populate-cache.yaml?style=flat-square)][github-workflow]

An up-to-date binary cache of [serokell/deploy-rs][deploy-rs].
Builds are generated nightly to ensure the latest version is always cached.

## System support
We try to support all the systems that deploy-rs does.

- [x] `x86_64-linux`
- [x] `aarch64-linux`
- [x] `x86_64-darwin`
- [x] `aarch64-darwin`

**Note:** the `aarch64-darwin` build is run on flyci's m1 macs, because they offer a free tier for open-source projects.

## Usage

### Flake-based system
To use the binary cache for nixos systems configured via flake, first
add the cache as a substituter and then trust the public key.
```nix
nix.settings = {
  substituters = [ "https://deploy-rs.cachix.org" ];
  trusted-public-keys = [ "deploy-rs.cachix.org-1:xfNobmiwF/vzvK1gpfediPwpdIP0rpDV2rYqx40zdSI=" ];
};
```

### Non-flake system
To use the binary cache, add it to your [`nix.conf`](https://nixos.org/manual/nix/stable/command-ref/conf-file.html).
```conf
extra-substituters = https://deploy-rs.cachix.org
extra-trusted-public-keys = deploy-rs.cachix.org-1:xfNobmiwF/vzvK1gpfediPwpdIP0rpDV2rYqx40zdSI=
```

### Per-flake configuration
Flakes can suggest `nix.conf` changes when evaluated via the top-level `nixosConfig` attribute.
To add the cache for users of your flake, add the following to your flake
```nix
{
  input = { ... };
  outputs = { ... };
  nixConfig = {
    extra-substituters = [ "https://deploy-rs.cachix.org" ];
    extra-trusted-public-keys = [ "deploy-rs.cachix.org-1:xfNobmiwF/vzvK1gpfediPwpdIP0rpDV2rYqx40zdSI=" ];
  };
}
```
