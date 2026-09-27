# Swedish Folkfriend (fork)

This is a fork of [FolkFriend](https://github.com/TomWyllie/folkfriend) by
Tom Wyllie, adapted to recognise and browse **Swedish traditional tunes**
instead of the original Irish/Scottish (thesession.org) repertoire.

- **Try it live:** https://swedishfolkfriend.netlify.app
- **Tune corpus:** scraped from [FolkWiki.se](http://www.folkwiki.se) (CC BY),
  see [`folkwiki-corpus/`](folkwiki-corpus/)
- **Original project:** https://github.com/TomWyllie/folkfriend /
  https://folkfriend.app

## What's different from upstream

- Tune index built from FolkWiki.se's ABC corpus
  (`folkwiki-corpus/build_index.py`) instead of thesession.org
- CLI: multi-channel WAV files are downmixed to mono before transcription
  (`rust/src/bin.rs`)
- Rust engine: settings are ordered by an explicit `order` field instead of
  assuming numeric setting IDs, since FolkWiki filenames aren't numeric
  (`rust/src/query/mod.rs`, `rust/src/index/schema.rs`)
- App: the tune index is bundled and always loaded from `/res/`, playback
  uses abcjs's built-in synth instead of the discontinued `midi` package,
  and tunes show a link back to their FolkWiki.se source page

## License

Like the original project, this repository is licensed under GPL-3.0 (see
[`LICENSE`](LICENSE)). The Swedish tune corpus in `folkwiki-corpus/` is
sourced from FolkWiki.se under CC BY; see individual `.meta.json` files for
per-tune attribution.

---

*Below is the original FolkFriend README:*

# FolkFriend
Scripts and Web Application for folk music tune transcription and recognition.

This is the Github repository for the FolkFriend app, for advanced users and developers of the app. If you are looking to simply use the web version of the app please instead go to [folkfriend.app](https://folkfriend.app). 

# Dependencies
- `rust` (for compiling the folkfriend library from source to run natively)
- `python 3.x` (for running some misc scripts, for example evaluating datasets)
- `wasm-pack` (for compiling the folkfriend library from source into WebAssembly)
- `Vue.js v2.x` (for frontend development)

I shall soon add some precompiled executables for windows + linux so compiling from source is not necessary to use the command line version of the library.

# Structure of Repository

| Directory | Description |
| ---       | ---         |
| `app/`| Source code and build scripts for the PWA hosted at [folkfriend.app](https://folkfriend.app) |
| `resources/`| Miscellaneous static assets |
| `rust/`| FolkFriend library source code (in rust) |
| `utils/`  | Contains the `folkfriend` module; python implementation of all the functionality that runs client-side in the app.

Note that if you are unfamiliar with rust, you can find implementations of all the key parts of FolkFriend in Python 3 in the commit history of this repository (I originally wrote FolkFriend in Python and learned rust as I went about translating into a WASM friendly language). The Python code is unmaintained and may be out of date.

# Using Rust

1. Install Rust
2. From the `rust/` directory of this repository, run `cargo build --release` to compile the `folkfriend` executable on your machine.
3. Add the `folkfriend` executable to your system path, for example by including a directory containing `folkfriend` to your path environment variable or by using `sudo cp folkfriend /usr/local/bin/`.
