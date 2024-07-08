# Rust Tools

Here's a list of common Rust tools I use in my projects. This is intended to be a list of things I should do - and it's opinionated.

## Cargo

### Verification

Tools that verify your project. Like tests, but for the rest of your stack.

- [`cargo-semver-checks`](https://github.com/obi1kenobi/cargo-semver-checks): A must-have plugin. Checks to see if you've [violated semantic versioning](https://doc.rust-lang.org/cargo/reference/semver.html) since your last Crates.io release.
- README Generators: Creates a README from your project's top-level doc comments. This means your README and `lib.rs` will never be out of sync. I have two suggestions - both are both well-received. Personally, I prefer `cargo-readme`, but `cargo-rdme` is great, too!
  - [`cargo-readme`](https://github.com/webern/cargo-readme): Directly creates a README from your `lib.rs` file. Allows for a quick setup, with templating for advanced users, but features limited configuration options.
  - [`cargo-rdme`](https://github.com/orium/cargo-rdme): Newer and uses configuration over templating. Provides more options but might be more complex.
- [`cargo-deny`](https://github.com/EmbarkStudios/cargo-deny): Checks your workspace's dependency tree for incompatible licenses, security vulnerabilities, and other potential issues.
- [`cargo-vet`](https://github.com/mozilla/cargo-vet): Helps make sure your dependencies have been audited by a trusted entity. Particularly **helpful in professional settings**.

### Testing

Tools to assist in testing your project's behavior.

- [`cargo-nextest`](https://nexte.st/): A harder, better, faster, stronger `cargo test`. Use it at all times.
- [`cargo-fuzz`](https://github.com/rust-fuzz/cargo-fuzz): Links with `libfuzzer` to fuzz (test a large range of values) in your project's user-facing API.
  - See [the usage guide here](https://rust-fuzz.github.io/book/cargo-fuzz/tutorial.html).
- [`cargo-all-features`](https://github.com/frewsxcv/cargo-all-features): Runs `cargo {build|check|test}` for all feature combinations. This ensures 100% coverage for weird feature flag combinations (and helps find [disallowed negative features](https://doc.rust-lang.org/cargo/reference/features.html#feature-unification)).
- [`cargo-mutants`](https://github.com/sourcefrog/cargo-mutants): Messes with your source code to make sure tests actually catch issues. It's much like fuzzing - except for your source code, not just a public API. **Use this!**
- [`cargo-husky`](https://github.com/rhysd/cargo-husky): When added to your project's `dev-dependencies`, this will ensure that a pre-commit hook is generated for `cargo-test`, ensuring that faulty code isn't pushed to your repo.
  - Keeps CI costs low, so potentially **good in limited workplace environments**.

### Building

Mostly for binaries, these tools assist in creating safe, solid releases for clients.

- [`cargo-auditable`](https://github.com/rust-secure-code/cargo-auditable): When building your binary, this tool emits dependency version information directly inside.
  - This **allows** large organizations, like **corporate clients, to scan binaries for announced vulnerabilities**, making Rust executables more trustworthy.
- [`cargo-dist`](https://opensource.axo.dev/cargo-dist/): Completely automates the process of creating new releases on GitHub and other platforms. It tags, builds, publishes, and announces your new release.
- [`cargo-chef`](https://github.com/LukeMathWalker/cargo-chef): Dramatically increases the speed of subsequent Docker builds for your project. **If you use Docker, this is a must-have.**

### Other

These don't fit elsewhere. But I like them!

- [`cargo-binstall`](https://github.com/cargo-bins/cargo-binstall): Installs Crates.io binaries from their linked repos' releases/artifacts sections. This can substantially speed up tooling installations, so it's always the first thing I get on a new machine.
- [`cargo-sweep`](https://github.com/holmgr/cargo-sweep): Cleans up `target/` folders recursively. If you write a lot of Rust, this can shave hundreds of gigabytes off your drives.
- [`cargo-machete`](https://github.com/bnjbvr/cargo-machete): Checks your project for unused dependencies.
- [`cargo-expand`](https://github.com/dtolnay/cargo-expand): Outputs full macro expansions within files. This can assist you in debugging weird macro behavior, but prepare for some verbosity...
- [`cargo-flamegraph`](https://github.com/flamegraph-rs/flamegraph): Runs your binary in release mode and outputs [a flamegraph](https://www.brendangregg.com/flamegraphs.html), which is just an SVG graph. Open in a browser and click on any box to see more detail!
- [`cargo-watch`](https://github.com/watchexec/cargo-watch): Wait for changes in your project folder, then do something when it's over.
  - For example, `cargo watch -x clippy` will continuously put `clippy` output into your terminal when you save.
  - Often, this is more readable than your IDE's errors.

## CI

TODO

## Libraries

TODO
