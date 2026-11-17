# Release and Composer workflow

## Branches and releases

- Maintain one branch per OXID minor line (`b-7.0` through `b-7.6`).
- Build each OXID release as its own commit and matching `vX.Y.Z` tag. Do not combine multiple upstream releases in one commit.
- Base a new minor branch on the latest FriendsOfOxid branch for the preceding minor line, then update its Composer dependencies to the corresponding OXID upstream release.
- Keep the branch's release commit limited to the compilation metadata and dependency changes; do not restore upstream CI workflows that this fork removed.

## Composer constraints

- Keep `oxid-esales/oxideshop-ce` pinned to the exact OXID release version.
- Use Composer `~` constraints for third-party dependencies so compatible patch updates can be installed without changing the shop core.
- When a dependency accepts multiple major lines, put `~` on every alternative, for example `~4.2.4 | ~5.0.1`.
- Keep optional integrations and modules in `suggest`, not `require`, so they are not installed by default.
- Preserve `friendsofoxid/security-advisories` in `require`.
- Preserve the FriendsOfOxid package identity, replacement of the official metapackage, and GPL license metadata.
- When importing upstream release dependency changes, retain the fork's constraint policy and optional-package treatment. Do not copy upstream `composer.json` wholesale.

## Release procedure

1. Inspect the upstream Composer changes for the target release.
2. Apply dependency additions, removals, and version updates to the fork while preserving the rules above.
3. Review the diff and ensure every new non-core version constraint uses `~` (including every alternative).
4. Commit the release with a message such as `add OXID 7.6.0 compilation`.
5. Create the matching `v7.6.0` tag on that commit.
6. Keep follow-up documentation or maintenance changes in separate commits.
