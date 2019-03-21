# Git pre-commit hook script for Drupal

## Overview

Git pre-commit hook script is been built specifically for Drupal git
repository.

## Prerequisite
1. PHP Code Sniffer (phpcs).
2. Coder module - `Drupal` code sniffer standard.

## Installation

1. For using this hook script just copy/download [this script file](https://github.com/sdemi/pre-commit/raw/master/pre-commit) to a directory called  `.githooks` in your root Drupal directory. Don't forget to give
executable permission for the script file.
2. Configure `core.hooksPath` variable to your your new managed hooks directory. In GitBash navigate to your root Drupal directory and execute the command `git config core.hooksPath .githooks`.
3. Instruct all remaining team members to pull in the new script using git and update the `core.hooksPath` variable using method above.

## Working

Whenever a git commit is been performed, pre-commit hook script will be executed
by git inbuilt hook support. The above script does syntax check, any debugging
function, merge conflict tags as well as looks for coding standard in the
changes staged to commit (which is a bad practice). In any case, the commit
operation will be aborted and can be committed after doing corrections or
removing the debugging function xfrom the code.

In case you want to force commit with any debugging functions (not recommended)
you can do it by using the git command option `-n OR --no-verify`.

### Syntax check

Syntax check is been performed using `php -l` command for each php files (file
with extensions 'php, inc and module').

### Check for debugging functions

Checking for debugging function is been performed using `git diff` command only
to files staged to commit and in turn only to added/modified changes.

List of debugging functions included for checking are: dpm, dpq, dvm,
ddebug_backtrace, print_r, var_dump, debug_backtrace, console.log. First 4
functions are of Drupal devel module, later 3 are of php and last one is of
javascript.

### Merge conflict marker check

Merge conflict marker check is been performed to all files staged to commit
using egrep pattern "(<<<<|====|>>>>)+.*(\n)?".

### Coding standard check

Checks for coding standard issues using `phpcs` with arguments:
1. standard = Drupal
2. extensions = 'php,module,inc,install,test,profile,theme,js,css,info,txt'

## Note
* Only two of the following directories will be checked for above violations:
  * /modules/custom/
  * /themes/custom/
* For better performance of the script, we have excluded the checking of files
with following extensions: 'info, png, gif, jpg, ico, patch, htaccess, sh, ttf,
woff, eot, svg'.
