
<p align="center">
    <img src="https://raw.githubusercontent.com/peckphp/peck/main/docs/logo.png" alt="Peck example" height="300">
    <p align="center">
        <a href="https://github.com/peckphp/peck/actions"><img alt="GitHub Workflow Status (master)" src="https://img.shields.io/github/actions/workflow/status/peckphp/peck/tests.yml"></a>
        <a href="https://packagist.org/packages/peckphp/peck"><img alt="Total Downloads" src="https://img.shields.io/packagist/dt/peckphp/peck"></a>
        <a href="https://packagist.org/packages/peckphp/peck"><img alt="Latest Version" src="https://img.shields.io/packagist/v/peckphp/peck"></a>
        <a href="https://packagist.org/packages/peckphp/peck"><img alt="License" src="https://img.shields.io/packagist/l/peckphp/peck"></a>
    </p>
</p>

------
**Peck** is a powerful CLI tool designed to identify wording or spelling mistakes in your codebase. Built for speed, simplicity, and seamless integration, Peck fits naturally into your workflow, much like tools such as Pint or Pest.

Leveraging the robust capabilities of **[GNU Aspell](https://en.wikipedia.org/wiki/GNU_Aspell)** via the [github.com/tigitz/php-spellchecker](https://github.com/tigitz/php-spellchecker) PHP wrapper, Peck inspects every corner of your codebase — including folder names, file names, method names, comments, and beyond — ensuring your work maintains a high standard of clarity and professionalism.

> Note: Peck is still under active development and is not yet ready for production use. Currently, only the filesystem checker is implemented, focusing exclusively on detecting spelling mistakes in file and folder names.

## Installation

> **Requires [PHP 8.3+](https://php.net/releases/) and [GNU Aspell](https://en.wikipedia.org/wiki/GNU_Aspell)**

Peck relies on GNU Aspell for its spell-checking functionality. Make sure Aspell is installed on your system before using Peck.

### Installing GNU Aspell

- **Debian/Ubuntu:**
    ```bash
    sudo apt-get install aspell aspell-en
    ```
    
- **MacOS (using Homebrew):**
    ```bash
    brew install aspell
    ```

- **Windows:**\
    > Move to WSL / WSL2, an use the following command:
    sudo apt-get install aspell aspell-en

    > If you are using native shells like powershell, etc, please lease refer to the [Aspell website](http://aspell.net/) for installation instructions.

### Installing Peck

You can require Peck using [Composer](https://getcomposer.org) with the following command:

```bash
composer require peckphp/peck --dev
```

## Usage

To check your project for spelling mistakes, run:

```bash
./vendor/bin/peck
```

### Command Options

The behaviour of `peck` can be modified with the following options:

##### `--config`

By default `peck` will check for a `peck.json` file in your project root. If one isn't available it will try to figure
out the directory to check by itself.

##### `--path`

The path to check can be overwritten with the `--path` option. If the path is one you always need checking you
can place it in your `peck.json` file. 

##### `--init`

If you don't have a `peck.json` file yet, you can create a blank configuration file by using the `--init` option.

## Configuration

Peck can be configured using a `peck.json` file in the root of your project. 

You can scaffold the `peck.json` file with:
```bash
./vendor/bin/peck --init
```

Here's an example configuration:

```json
{
    "ignore": {
        "words": [
            "config",
            "namespace"
        ],
        "directories": [
            "app/MyNamespace"
        ]
    }
}
```

You can also specify the path to the configuration file using the `--config` option:

```bash
./vendor/bin/peck --config relative/path/to/peck.json
```

## Running Peck on GitHub Actions

When running Peck on GitHub Actions, you can use the following workflow or something similar:

```yaml
- name: Install Aspell
    shell: bash
    run: |
        if [[ "$RUNNER_OS" == "Linux" ]]; then
            sudo apt-get update && sudo apt-get install -y aspell aspell-en
        elif [[ "$RUNNER_OS" == "macOS" ]]; then
            brew install aspell
        fi
```

---

Peck is an open-sourced software licensed under the **[MIT license](https://opensource.org/licenses/MIT)**.
