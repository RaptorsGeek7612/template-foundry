# Contributing

1. Fork the repo and create a branch from `master`.
2. `git submodule update --init --recursive` (or `forge install` if `lib/` is empty)
3. Make your changes, then run the full check before opening a PR:
   ```shell
   forge fmt --check
   forge build
   forge test
   ```
4. Open a pull request describing the change (the PR template will guide you). CI (GitHub Actions) must pass — it runs the same fmt/build/test steps.
