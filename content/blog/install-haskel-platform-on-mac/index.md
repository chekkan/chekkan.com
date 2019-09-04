Head over to https://www.haskell.org/platform/

The notes will tell you to 
> The recommended way to install the components of the mac platform is using [ghcup](https://www.haskell.org/ghcup) to install ghc and cabal-install.

**ghcup** is an installer for the general purpose language **Haskell**

Open a terminal and execute the following command to install `ghcup`

```
curl https://get-ghcup.haskell.org -sSf | sh
```
Press ENTER -> ENTER -> YES and ENTER to accept the prompts in terminal

[https://gitlab.haskell.org/haskell/ghcup/blob/master/README.md#manual-install]()

```
# prepare your environment
. "$HOME/.ghcup/env"
```

You should now be able to execute `cabal` and `ghcup` into your terminal.

```
echo '. $HOME/.ghcup/env' >> "$HOME/.bashrc"
```
or
```
echo '. $HOME/.ghcup/env' >> "$HOME/.zshrc"
```
makes sure that the environment variables are setup on new terminal windows.

Follow the instruction on [haskellstack.org](https://docs.haskellstack.org/en/stable/README/) to install stack.

If you have homebrew...
```
brew install haskell-stack
```
