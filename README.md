# Tech Demo: Build Custom JFrog CLI (bonus: contributing back)

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

### Option 3a: Use the build.sh
Make any changes you like to the code. The [jfrog-cli](./jfrog-cli) depends on the [jfrog-cli-core](./jfrog-cli-core). This custom version already has the most basic changes you need to get started and begin at a version Aaron has confirmed will compile together.

Then run the build command:

```sh
cd ./jfrog-cli
./build/build.sh
```

### Option 3b: Use go install

As long as you have included the `$GOPATH/bin` in your `$PATH` and it has higher precedence than the directory the normal `jf` executable gets installed in. However, like most things, [you can control this too](https://pkg.go.dev/cmd/go#hdr-GOPATH_environment_variable) if you need to.

```sh
go install
```

## Step 4: Create a local bin

If you used option 3b, then you don't need to go further. Following along further is useful for creating a directory to store aliased (symlink) binaries or custom built executables.

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

### 1. Fork this repository

If you have the GH CLI and this repo cloned locally, simply:

```sh
gh repo fork
```

Otherwise, you can do it through [the GitHub UI](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo).

### 2. Fork JFrog CLI Repositories

#### A. GH CLI

```sh
git submodule foreach 'gh repo fork --clone=false --remote=true'
```

#### B. Manually

- https://github.com/jfrog/build-info-go
- https://github.com/jfrog/jfrog-cli
- https://github.com/jfrog/jfrog-cli-artifactory
- https://github.com/jfrog/jfrog-cli-core
- https://github.com/jfrog/jfrog-cli-platform-services
- https://github.com/jfrog/jfrog-cli-security
- https://github.com/jfrog/jfrog-client-go

Fork the above repos to your GitHub account.

Then you can update the [.gitmodules](.gitmodules) and run `git submodule sync --recursive` or run `git submodule set-url` (see: [docs](https://git-scm.com/docs/git-submodule#Documentation/git-submodule.txt-set-url--ltpathgtltnewurlgt))
