# Terraform Module for Self-Extractable Archive

This module creates a self-extractable archive from a directory using [makeself](https://makeself.io/). The archive can be used to bootstrap a new instance using cloud-init.

Module uses `external` provider to run `makeself` command. It creates temporary directory, copies source directory to it, runs `makeself` and returns path to the archive.

Module targets to build hermetic self-extractable archives. It uses `--nomd5 --nocrc` options to disable checksums.

## Usage

Quick start:

```terraform
module "bootstrap" {
  source      = "andreygubarev/self-extractable-archive/external"
  source_dir = "${path.module}/bootstrap"
}
```

Advanced usage:

```terraform
module "bootstrap" {
  source  = "andreygubarev/self-extractable-archive/external"
  version = "1.2.0"

  label          = "bootstrap"                 # Description of the archive
  source_dir     = "${path.module}/bootstrap"  # Directory to be archived
  entrypoint     = "entrypoint.sh"             # Entrypoint script, relative to source_dir, defaults to "entrypoint.sh"
  file_name      = "bootstrap.run"             # Name of self-extractable archive
}
```

## Prerequisite

For MacOS:
```bash
brew install gnu-tar
export PATH="/opt/homebrew/opt/gnu-tar/libexec/gnubin:$PATH"
```



# Reference

- https://makeself.io/
- https://registry.terraform.io/providers/hashicorp/external/latest
