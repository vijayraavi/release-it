# Publish to npm

With a `package.json` in the current directory, release-it will let `npm` bump the version in `package.json` (and
`package-lock.json` if present), and publish to the npm registry.

## Tags

Use e.g. `--npm.tag=beta` to tag the package in the npm repository. With the `--preRelease=beta` shorthand, the npm
dist-tag will have the same value (unless `--npm.tag` is used to override this). The default tag is "latest".

For a pre-release, the default tag is "next". The tag will be derived from the pre-release version (e.g. version
`2.0.0-alpha.3` will result in tag "alpha"), unless overridden by setting `npm.tag`.

## Public scoped packages

A [scoped package](https://docs.npmjs.com/misc/plugin) (e.g. `@user/package`) is either public or private. To
[publish scoped packages](https://docs.npmjs.com/misc/plugin#publishing-scoped-packages), make sure this is in
`package.json`:

```json
{
  "publishConfig": {
    "access": "public"
  }
}
```

By default, `npm publish` will
[publish a scoped package as private](https://docs.npmjs.com/creating-and-publishing-private-packages) (requires paid
account).

## Two-factor authentication

In case two-factor authentication (2FA) is enabled for the package, release-it will ask for the one-time password (OTP).

The OTP can be provided from the command line (`--npm.otp=123456`). However, providing the OTP without a prompt
basically defeats the purpose of 2FA (also, the OTP expires after a short period).

## Monorepos

Monorepos do not require extra configuration, but release-it handles only one package at a time. Also see how
[Git steps can be skipped](#skip-git-steps) (e.g. if tagging the Git repo should be skipped).

## Miscellaneous

- Learn how to [authenticate and publish from a CI/CD environment](./ci.md#npm).
- The `"private": true` setting in package.json will be respected, and `release-it` will skip this step.
- Getting an `ENEEDAUTH` error while a manual `npm publish` works? Please see
  [#95](https://github.com/release-it/release-it/issues/95#issuecomment-344919384).
