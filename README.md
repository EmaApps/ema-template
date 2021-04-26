# Ema Template

This repository represents a **real-world example** of [Ema](https://ema.srid.ca/) — it is the source for ema.srid.ca website — and as such acts as a **template repository** to use for bootstrapping your next static site using Ema.

## Getting Started

To develop with full IDE support in Visual Studio Code, follow these steps:

- [Install Nix](https://nixos.org/download.html) & [enable Flakes](https://nixos.wiki/wiki/Flakes)
- Run `nix-shell --run haskell-language-server` to sanity check your environment 
- Open as folder in Visual Studio Code
    - Install the recommended extensions
    - <kbd>Ctrl+Shift+P</kbd> to run command "Nix-Env: Select Environment" and select `shell.nix`. The extension will ask you to reload VSCode at the end.
- Press <kbd>Ctrl+Shift+B</kbd> in VSCode, or run `bin/run` in terminal, to launch the Ema dev server.

All steps above except the last one need to be done only once.

## Note

- This project uses [relude](https://github.com/kowainik/relude) as its prelude, as well as [Tailwind+Blaze](https://ema.srid.ca/guide/tailwind) for CSS framework and HTML DSL. Even though the author highly recommends them, you are of course free to swap them out for the library of your choice.
- As a first step to using this template, 
  - change the project name in .cabal, .flake and hie.yaml files.
  - Change the `cname` in .github/workflows/publish.yaml, or remove it to publish to yourname.github.io
- To change the port, see file bin/run
- To change the CLI arguments, see file .ghcid
- To update Ema to latest Git revision, run `nix flake lock --update-input ema`
- To add/remove Haskell dependencies, see the .cabal file. If a dependency is unavailable in nixpkgs, you can override it (to point to say a Git repo) in the `overrides` attribute of flake.nix. You can imitate the manner in which the `ema` package itself is overriden.