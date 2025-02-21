# PS Tech Demo: Build JFrog CLI from source

Welcome to Aaron's opinionated way to build and run the JFrog CLI from source.

## Step 1: Project setup

```sh
git clone "this repository URL" jfrog-cli-dev
cd jfrog-cli-dev
git submodule update --init --recursive
```

## Step 2: Open VSCode

```sh
open -a "Visual Studio Code" .
```

### Bonus 1: ZSH/MacOS alias for vscode

If you have ever used vscode on Windows or Linux, you may have enjoyed being able to type `code .` in any folder to open it in vscode. Now it is here on MacOS:

Add this to your `~/.zsh_aliases`:
```sh
alias code='open -a "Visual Studio Code" --'
```

Then the Step 2 simply becomes:

```sh
code .
```

## Step 3: Build the CLI

Make any changes you like to the code. The [jfrog-cli](./jfrog-cli) depends on the [jfrog-cli-core](./jfrog-cli-core). This custom version already has the most basic changes you need to get started and begin at a version Aaron has confirmed will compile together.

Then run the build command:

```sh
cd ./jfrog-cli
./build/build.sh
```

## Step 4: Create a local bin

Useful for aliasing (symlink) binaries or custom built executables.

```sh
mkdir -p ~/.local/bin/
```

## Step 5: Alias using the local bin

### Option A: Symlink the binary

Set and forget.

```sh
ln -s "$PWD/jf" ~/.local/bin/jf
```

### Option B: Copy the binary

Consciously update.

```sh
cp -vp ./jf ~/.local/bin/
```

## Step 6: Run

I recommend customizing the JF version (`CliVersion`) in the [cli_consts.go](./jfrog-cli/utils/cliutils/cli_consts.go) so you know it is custom:

```sh
jf -v
```

Example:

```
jf version 2.73.2-aaronc.0
```

## Bonus: Personal Forks for Upstream Contribution

1. Fork this repository (perhaps as `jfrog-cli-dev` or similar), the [jfrog/jfrog-cli](https://github.com/jfrog/jfrog-cli/), & [jfrog/jfrog-cli-core](https://github.com/jfrog/jfrog-cli-core/) to your GitHub account.
2. Add a remote to your local repository and push everything to your fork.
3. Update the [.gitmodules](.gitmodules) to point to your fork's remote and reinitialize.
    ```sh
    git clean -xfdf
    git submodule update --init --recursive
    ```