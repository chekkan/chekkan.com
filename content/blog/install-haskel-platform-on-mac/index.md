---
title: Install haskell platform on mac with homebrew
date: "2019-09-05T00:30:00.000Z"
tags:
  - haskell
---

Head over to [haskell.org](https://www.haskell.org/platform/)

> The recommended way to install the components of the mac platform is using [ghcup](https://www.haskell.org/ghcup) to install ghc and cabal-install.

**ghcup** is an installer for the general purpose language **Haskell**

Open a terminal and execute the following command to install `ghcup`

```shell
curl https://get-ghcup.haskell.org -sSf | sh
```

Press `ENTER` -> `ENTER` -> type `YES` and `ENTER` to accept the prompts in terminal.

[ghcup README](https://gitlab.haskell.org/haskell/ghcup/blob/master/README.md)

```shell
# prepare your environment
. "$HOME/.ghcup/env"
```

You should now be able to execute `cabal` and `ghcup` into your terminal.

```shell
echo '. $HOME/.ghcup/env' >> "$HOME/.bashrc"
```
or
```shell
echo '. $HOME/.ghcup/env' >> "$HOME/.zshrc"
```
makes sure that the environment variables are setup on new terminal windows.

Follow the instruction on [haskellstack.org](https://docs.haskellstack.org/en/stable/README/) to install stack.

If you have homebrew...
```shell
brew install haskell-stack
```
