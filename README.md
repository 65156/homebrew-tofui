# homebrew-tofui

Homebrew tap for [tofUI](https://github.com/65156/tofUI) — beautiful OpenTofu & Terraform plan reports.

## Install

```sh
brew tap 65156/tofui
brew install tofui
```

Or in one line without tapping first:

```sh
brew install 65156/tofui/tofui
```

> **Homebrew 6.0+** requires trusting third-party taps. If you see
> `Refusing to load formula … from untrusted tap`, run `brew trust 65156/tofui`
> (or `brew trust --formula 65156/tofui/tofui`) and re-run the install.

Everything (report generation, dashboard publishing, and S3 hosting) is bundled —
`requests` and `boto3` ship inside the formula's isolated virtualenv, so no extra
steps are needed.

## Upgrade

```sh
brew update
brew upgrade tofui
```

## Uninstall

```sh
brew uninstall tofui
brew untap 65156/tofui
```

## Maintainers: cutting a new release

When a new `tofUI` version is tagged on GitHub:

1. Bump `url` in `Formula/tofui.rb` to the new tag tarball and update its `sha256`:
   ```sh
   curl -sL https://github.com/65156/tofUI/archive/refs/tags/vX.Y.Z.tar.gz | shasum -a 256
   ```
2. Refresh the Python `resource` blocks if dependencies changed:
   ```sh
   brew update-python-resources 65156/tofui/tofui
   ```
3. Verify locally:
   ```sh
   brew audit --formula 65156/tofui/tofui
   brew install --build-from-source 65156/tofui/tofui
   brew test 65156/tofui/tofui
   ```
4. Commit and push.
