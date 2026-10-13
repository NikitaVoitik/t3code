# T3 Code fork

Personal build of [pingdotgg/t3code](https://github.com/pingdotgg/t3code) nightly with extra commits.

- **`custom`**: upstream `main` plus this fork's commits. Put your changes here.
- **`fork`** (default branch): only the mirror workflow. Upstream's own workflows never run here.
- **Releases**: [`mirror-nightly.yml`](.github/workflows/mirror-nightly.yml) rebuilds each upstream nightly with the `custom` commits on top, for macOS arm64. It uses the same tag and version, signs with the self-signed certificate in the `MACOS_SELF_SIGN_*` secrets, and publishes here. The desktop update button follows these releases. Servers update from npm to the same version.

## Changing the fork

```sh
git fetch upstream
git switch custom
git rebase upstream/main      # keep custom current with upstream
# ...commit your changes...
git push --force-with-lease origin custom
```

The next scheduled run (every 2 hours), or **Actions → Mirror upstream nightly → Run workflow**, builds the latest upstream nightly with your commits. If they stop applying, the workflow opens an issue.

## Signing

The macOS app is signed with a self-signed certificate. The first install needs **System Settings → Privacy & Security → Open Anyway**. Updates go through the update button. If the certificate secrets are ever replaced, reinstall once by hand from the latest release.
