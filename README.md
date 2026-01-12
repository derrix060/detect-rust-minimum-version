# README

This README provides information about the `detect-rust-minimum-version` action.

## Description

The `detect-rust-minimum-version` action is a GitHub Action that detects the minimum required version of Rust for a Rust project. It scans the project's source code and analyzes the `Cargo.toml` file to determine the minimum required version.

## Usage

To use this action, you can include it in your workflow file as follows:

```yaml
name: Detect Rust Minimum Version

on:
    push:
        branches:
            - main

jobs:
    detect-rust-minimum-version:
        runs-on: ubuntu-latest

        steps:
            - name: Checkout repository
              uses: actions/checkout@v4

            - name: Detect Rust Minimum Version
              id: rust-version
              uses: derrix060/detect-rust-minimum-version@v2
              with:
                repos: repo/my-path1,repo/my-path2
                locked: true  # Enforce using Cargo.lock
                min: "1.78.0"  # Minimum Rust version to start searching from.
            
            - name: Print version
              run: echo "Minimum rust version is ${{ steps.rust-version.outputs.highest-msrv }}"
```

## Inputs

- `paths` (optional): A comma-separated list of relative paths to the directories or files that should be scanned for detecting the minimum required version of Rust. If not provided, the action will default to the current location.
- `locked` (optional): If true, passes --locked to cargo to enforce using Cargo.lock and prevent dependency re-resolution.
- `min` (optional): The minimum Rust version to start searching from. Useful when Cargo.lock uses v4 format (requires 1.78.0+).

## Outputs

- `highest-msrv`: The highest minimum Rust version required, based on a AND operation on all paths.  It basically means that it is the highest msrv for all the paths.

## License

This action is licensed under the [MIT License](LICENSE).
