# @tummycrypt/tinyland-ip-bans (retired)

This repository is retired and archived (2026-10-10, estate uplift rulings
RU2, RU6, RU7, RU8).

Its code now lives in
[xoxd-ai/tinyland-security](https://github.com/xoxd-ai/tinyland-security) as
the `./ip-bans` subpath export of `@tummycrypt/tinyland-security`, starting
with tinyland-security 1.0.0. The API is unchanged: `configureIpBans`,
`getIpBansConfig`, `resetIpBansConfig`, `isIpBanned`, `addIpBan`,
`removeIpBan`, `deactivateIpBan`, `getActiveBans`, `cleanupExpiredBans` and
the `IpBan`, `AddIpBanOptions`, `IpBansLogger` and `IpBansConfig` types.

## Migrating

1. In `MODULE.bazel`, replace
   `bazel_dep(name = "tummycrypt_tinyland_ip_bans", ...)` with
   `bazel_dep(name = "tummycrypt_tinyland_security", version = "1.0.0")`
   from [xoxd-ai/bazel-registry](https://github.com/xoxd-ai/bazel-registry),
   and link `@tummycrypt_tinyland_security//:pkg` with `npm_link_package`.
2. Change imports (and `vi.mock` targets) from
   `@tummycrypt/tinyland-ip-bans` to `@tummycrypt/tinyland-security/ip-bans`.
   Use the subpath, not the root entry: the root of tinyland-security
   exports an older ban store with the same function names
   (`configureIpBanStore`), which keeps its own configuration.
3. tinyland-security 1.0.0 is built with TypeScript 7.0.2 (RU1); move the
   consumer to the same stack in the same change.

The registry module `tummycrypt_tinyland_ip_bans` is marked deprecated.
Its 0.2.2 and 0.2.3 entries stay resolvable and nothing is yanked, so
existing pins keep building until they move. The package is no longer
published to npm or GitHub Packages; the publish workflow is removed.
