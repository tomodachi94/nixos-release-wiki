# EOL cleanup

The old release reaches its end of life one month after the new release
gets released. At that point a few cleanup tasks need to be done.

1. Set the EOL channel status from `deprecated` to `unmaintained` in `infra`. Examples:
    - [channels: Deprecate NixOS 22.05](https://github.com/NixOS/infra/pull/229)
    - [channels: Mark 21.11 as unmaintained](https://github.com/NixOS/infra/pull/211)
    - [channels:21.05 is unmaintained](https://github.com/NixOS/infra/pull/201)

1. Once this is merged, update the [`nixos-search`](https://github.com/NixOS/nixos-search)
   repository to reflect that status on [search.nixos.org](https://search.nixos.org).

   ```bash
   nix --extra-experimental-features "nix-command flakes" flake lock --update-input nixos-infra
   ```

1. Close all pull requests that target one of the the old release- or staging-branches

1. Prune old [backport labels](https://github.com/NixOS/nixpkgs/labels?q=backport)

1. Remove the link to the EOL version's changelog from [`.github/PULL_REQUEST_TEMPLATE.md`](https://github.com/NixOS/nixpkgs/blob/master/.github/PULL_REQUEST_TEMPLATE.md)

1. Remove the old release from the [periodic merge workflows](https://github.com/NixOS/nixpkgs/commit/8befefd1a72da597bdb1d01e97127e0c9866912e)

1. Increase the `oldestSupportedRelease` in `lib/trivial.nix` to match
   the oldest supported release.

   Examples: [22.05](https://github.com/NixOS/nixpkgs/pull/180152)
