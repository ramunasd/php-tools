# Local php tools

This ansible role installs local development tools and creates links, wrappers and auto configuration files for more
convenient usage.
 
# Requirements

Globally installed composer and git is required.

# Installation

Just run `ansible-playbook playbook.yml` and enjoy!
 
# Tools

By default all development tools is installed to `~/.local/share`. You can change this by defining another default path
in role configuration. For more info look at [defaults](defaults/main.yml).

## Default tools

This means tool doesn't have any predefined configurations or options.

* parallel-lint
* pdepend
* phpcpd
* php-cs-fixer
* phpdcd
* phploc
* phpmd
* phpspec
* puli
* yaml-lint

## Predefined configuration

* phpcs `--standard=psr2`
* xdebug `-dzend_extension=xdebug.so -dxdebug.remote_enable=1 -dxdebug.max_nesting_level=200 -dxdebug.coverage_enable=0`
  This wrapper lets you disable xdebug in global php configuration. You can use this wrapper in fron of any other script,
  i.e. `xdebug app/console ...`.
* xml-lint `--exclude vendors`

## Automatic configuration

It's special wrappers which tries to detect local configuration file, and if it exists, use it. Otherwise wrappers acts
like standard executables.

* phpunit `-c .config/phpunit/config.xml`
* xphpunit - same as phpunit, but with xdebug enabled, useful for debugging failing tests
* xcoverage - same as xphpunit, but with code coverage enabled, useful if you are generating coverage locally
* xprofile - same as xdebug, but with enabled profiler, dumps is placed in same dir

# Hooks

This role installs default git hooks into ~/.git_hooks. This place is used by tool [git-hooks](https://github.com/icefox/git-hooks)
so you can install all hooks very easily just by running command `git hooks --install` inside your project dir.

## Available hooks

* pre-commit/10-php-lint - lint changed php files
* pre-commit/20-phpcs - check code style according to psr2 standard
