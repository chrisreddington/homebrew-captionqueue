# homebrew-captionqueue

Homebrew tap for [CaptionQueue](https://github.com/chrisreddington/captionqueue).

## Install

```bash
brew tap chrisreddington/captionqueue
brew install captionqueue
```

Or in one shot:

```bash
brew install chrisreddington/captionqueue/captionqueue
```

This installs the `captionqueue` CLI plus its system dependency `ffmpeg`. The
optional `[transcribe]` extra (Foundry Local + Nemotron) is **not** bundled —
install it separately with `pipx inject captionqueue foundry-local-sdk` if you
need local transcription.

## Upgrade / uninstall

```bash
brew upgrade captionqueue
brew uninstall captionqueue
brew untap chrisreddington/captionqueue   # optional
```

## How releases land here

This tap is updated automatically. When a new tag is pushed in
`chrisreddington/captionqueue`, that repo's release workflow fires a
`repository_dispatch` event of type `captionqueue_release` at this repo.
[`.github/workflows/release-dispatch.yml`](.github/workflows/release-dispatch.yml)
then:

1. Downloads the published sdist from PyPI and verifies its SHA-256.
2. Rewrites `Formula/captionqueue.rb` with the new `url`, `sha256`, and `version`.
3. Refreshes the Python `resource` blocks from PyPI via
   `brew update-python-resources`.
4. Audits and installs the formula on a macOS runner to verify it builds.
5. Commits the updated formula to `main`.

The formula is intentionally simple: a Python virtualenv install with `ffmpeg`
as a runtime dependency. The first release will populate the placeholder
`url`/`sha256`/`version` values in `Formula/captionqueue.rb`.
