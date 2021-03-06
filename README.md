# The Fuck [![Build Status](https://travis-ci.org/nvbn/thefuck.svg?branch=master)](https://travis-ci.org/nvbn/thefuck) 

Magnificent app which corrects your previous console command,
inspired by a [@liamosaur](https://twitter.com/liamosaur/)
[tweet](https://twitter.com/liamosaur/status/506975850596536320).

[![gif with examples](https://raw.githubusercontent.com/nvbn/thefuck/master/example.gif)](https://raw.githubusercontent.com/nvbn/thefuck/master/example.gif)

Few more examples:

```bash
➜ apt-get install vim
E: Could not open lock file /var/lib/dpkg/lock - open (13: Permission denied)
E: Unable to lock the administration directory (/var/lib/dpkg/), are you root?

➜ fuck
sudo apt-get install vim [enter/↑/↓/ctrl+c]
[sudo] password for nvbn:
Reading package lists... Done
...
```

```bash
➜ git push
fatal: The current branch master has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin master


➜ fuck
git push --set-upstream origin master [enter/↑/↓/ctrl+c]
Counting objects: 9, done.
...
```

```bash
➜ puthon
No command 'puthon' found, did you mean:
 Command 'python' from package 'python-minimal' (main)
 Command 'python' from package 'python3' (main)
zsh: command not found: puthon

➜ fuck
python [enter/↑/↓/ctrl+c]
Python 3.4.2 (default, Oct  8 2014, 13:08:17)
...
```

```bash
➜ git brnch
git: 'brnch' is not a git command. See 'git --help'.

Did you mean this?
	branch

➜ fuck
git branch [enter/↑/↓/ctrl+c]
* master
```

```bash
➜ lein rpl
'rpl' is not a task. See 'lein help'.

Did you mean this?
         repl

➜ fuck
lein repl [enter/↑/↓/ctrl+c]
nREPL server started on port 54848 on host 127.0.0.1 - nrepl://127.0.0.1:54848
REPL-y 0.3.1
...
```

If you are not scared to blindly run the changed command, there is a `require_confirmation`
[settings](#settings) option:

```bash
➜ apt-get install vim
E: Could not open lock file /var/lib/dpkg/lock - open (13: Permission denied)
E: Unable to lock the administration directory (/var/lib/dpkg/), are you root?

➜ fuck
sudo apt-get install vim
[sudo] password for nvbn:
Reading package lists... Done
...
```

## Requirements

- python (2.7+ or 3.3+)
- pip
- python-dev

## Installation

Install `The Fuck` with `pip`:

```bash
sudo pip install thefuck
```

[Or using an OS package manager (OS X, Ubuntu, Arch).](https://github.com/nvbn/thefuck/wiki/Installation)

You should place this command in your `.bash_profile`, `.bashrc`, `.zshrc` or other startup script:

```bash
eval "$(thefuck --alias)"
# You can use whatever you want as an alias, like for Mondays:
eval "$(thefuck --alias FUCK)"
```

[Or in your shell config (Bash, Zsh, Fish, Powershell, tcsh).](https://github.com/nvbn/thefuck/wiki/Shell-aliases)

Changes will be available only in a new shell session.
To make them available immediately, run `source ~/.bashrc` (or your shell config file like `.zshrc`).


## Update

```bash
sudo pip install thefuck --upgrade
```

**Aliases changed in 1.34.**

## How it works

The Fuck tries to match a rule for the previous command, creates a new command
using the matched rule and runs it. Rules enabled by default are as follows:

* `cargo` &ndash; runs `cargo build` instead of `cargo`;
* `cargo_no_command` &ndash; fixes wrongs commands like `cargo buid`;
* `cd_correction` &ndash; spellchecks and correct failed cd commands;
* `cd_mkdir` &ndash; creates directories before cd'ing into them;
* `cd_parent` &ndash; changes `cd..` to `cd ..`;
* `composer_not_command` &ndash; fixes composer command name;
* `cp_omitting_directory` &ndash; adds `-a` when you `cp` directory;
* `cpp11` &ndash; adds missing `-std=c++11` to `g++` or `clang++`;
* `dirty_untar` &ndash; fixes `tar x` command that untarred in the current directory;
* `dirty_unzip` &ndash; fixes `unzip` command that unzipped in the current directory;
* `django_south_ghost` &ndash; adds `--delete-ghost-migrations` to failed because ghosts django south migration;
* `django_south_merge` &ndash; adds `--merge` to inconsistent django south migration;
* `docker_not_command` &ndash; fixes wrong docker commands like `docker tags`;
* `dry` &ndash; fixes repetitions like `git git push`;
* `fix_alt_space` &ndash; replaces Alt+Space with Space character;
* `fix_file` &ndash; opens a file with an error in your `$EDITOR`;
* `git_add` &ndash; fixes *"Did you forget to 'git add'?"*;
* `git_branch_delete` &ndash; changes `git branch -d` to `git branch -D`;
* `git_branch_list` &ndash; catches `git branch list` in place of `git branch` and removes created branch;
* `git_checkout` &ndash; fixes branch name or creates new branch;
* `git_diff_staged` &ndash; adds `--staged` to previous `git diff` with unexpected output;
* `git_fix_stash` &ndash; fixes `git stash` commands (misspelled subcommand and missing `save`);
* `git_not_command` &ndash; fixes wrong git commands like `git brnch`;
* `git_pull` &ndash; sets upstream before executing previous `git pull`;
* `git_pull_clone` &ndash; clones instead of pulling when the repo does not exist;
* `git_push` &ndash; adds `--set-upstream origin $branch` to previous failed `git push`;
* `git_push_pull` &ndash; runs `git pull` when `push` was rejected;
* `git_stash` &ndash; stashes you local modifications before rebasing or switching branch;
* `go_run` &ndash; appends `.go` extension when compiling/running Go programs
* `grep_recursive` &ndash; adds `-r` when you trying to `grep` directory;
* `gulp_not_task` &ndash; fixes misspelled gulp tasks;
* `has_exists_script` &ndash; prepends `./` when script/binary exists;
* `heroku_not_command` &ndash; fixes wrong `heroku` commands like `heroku log`;
* `history` &ndash; tries to replace command with most similar command from history;
* `java` &ndash; removes `.java` extension when running Java programs;
* `javac` &ndash; appends missing `.java` when compiling Java files;
* `lein_not_task` &ndash; fixes wrong `lein` tasks like `lein rpl`;
* `ls_lah` &ndash; adds `-lah` to `ls`;
* `man` &ndash; changes manual section;
* `man_no_space` &ndash; fixes man commands without spaces, for example `mandiff`;
* `mercurial` &ndash; fixes wrong `hg` commands;
* `mkdir_p` &ndash; adds `-p` when you trying to create directory without parent;
* `no_command` &ndash; fixes wrong console commands, for example `vom/vim`;
* `no_such_file` &ndash; creates missing directories with `mv` and `cp` commands;
* `open` &ndash; prepends `http` to address passed to `open`;
* `pip_unknown_command` &ndash; fixes wrong `pip` commands, for example `pip instatl/pip install`;
* `python_command` &ndash; prepends `python` when you trying to run not executable/without `./` python script;
* `python_execute` &ndash; appends missing `.py` when executing Python files;
* `quotation_marks` &ndash; fixes uneven usage of `'` and `"` when containing args'
* `rm_dir` &ndash; adds `-rf` when you trying to remove directory;
* `sed_unterminated_s` &ndash; adds missing '/' to `sed`'s `s` commands;
* `sl_ls` &ndash; changes `sl` to `ls`;
* `ssh_known_hosts` &ndash; removes host from `known_hosts` on warning;
* `sudo` &ndash; prepends `sudo` to previous command if it failed because of permissions;
* `switch_lang` &ndash; switches command from your local layout to en;
* `systemctl` &ndash; correctly orders parameters of confusing `systemctl`;
* `test.py` &ndash; runs `py.test` instead of `test.py`;
* `tsuru_login` &ndash; runs `tsuru login` if not authenticated or session expired;
* `tsuru_not_command` &ndash; fixes wrong `tsuru` commands like `tsuru shell`;
* `tmux` &ndash; fixes `tmux` commands;
* `unknown_command` &ndash; fixes hadoop hdfs-style "unknown command" for example adds missing '-' to the command on `hdfs dfs ls`;
* `whois` &ndash; fixes `whois` command.

Enabled by default only on specific platforms:

* `apt_get` &ndash; installs app from apt if it not installed;
* `brew_install` &ndash; fixes formula name for `brew install`;
* `brew_unknown_command` &ndash; fixes wrong brew commands, for example `brew docto/brew doctor`;
* `brew_upgrade` &ndash; appends `--all` to `brew upgrade` as per Homebrew's new behaviour;
* `pacman` &ndash; installs app with `pacman` if it is not installed (uses `yaourt` if available).
* `pacman_not_found` &ndash; fix package name with `pacman` or `yaourt`;

Bundled, but not enabled by default:

* `git_push_force` &ndash; adds `--force` to a `git push` (may conflict with `git_push_pull`);
* `rm_root` &ndash; adds `--no-preserve-root` to `rm -rf /` command.

## Creating your own rules

For adding your own rule you should create `your-rule-name.py`
in `~/.thefuck/rules`. The rule should contain two functions:

```python
match(command: Command, settings: Settings) -> bool
get_new_command(command: Command, settings: Settings) -> str | list[str]
```

Also the rule can contain an optional function

```python
side_effect(old_command: Command, fixed_command: str, settings: Settings) -> None
```
and optional `enabled_by_default`, `requires_output` and `priority` variables.

`Command` has three attributes: `script`, `stdout` and `stderr`.

`Settings` is a special object filled with `~/.thefuck/settings.py` and values from env ([see more below](#settings)).

Simple example of the rule for running script with `sudo`:

```python
def match(command, settings):
    return ('permission denied' in command.stderr.lower()
            or 'EACCES' in command.stderr)


def get_new_command(command, settings):
    return 'sudo {}'.format(command.script)

# Optional:
enabled_by_default = True

def side_effect(command, settings):
    subprocess.call('chmod 777 .', shell=True)

priority = 1000  # Lower first, default is 1000

requires_output = True
```

[More examples of rules](https://github.com/nvbn/thefuck/tree/master/thefuck/rules),
[utility functions for rules](https://github.com/nvbn/thefuck/tree/master/thefuck/utils.py).

## Settings

The Fuck has a few settings parameters which can be changed in `~/.thefuck/settings.py`:

* `rules` &ndash; list of enabled rules, by default `thefuck.conf.DEFAULT_RULES`;
* `require_confirmation` &ndash; requires confirmation before running new command, by default `True`;
* `wait_command` &ndash; max amount of time in seconds for getting previous command output;
* `no_colors` &ndash; disable colored output;
* `priority` &ndash; dict with rules priorities, rule with lower `priority` will be matched first;
* `debug` &ndash; enables debug output, by default `False`.

Example of `settings.py`:

```python
rules = ['sudo', 'no_command']
require_confirmation = True
wait_command = 10
no_colors = False
priority = {'sudo': 100, 'no_command': 9999}
debug = False
```

Or via environment variables:

* `THEFUCK_RULES` &ndash; list of enabled rules, like `DEFAULT_RULES:rm_root` or `sudo:no_command`;
* `THEFUCK_REQUIRE_CONFIRMATION` &ndash; require confirmation before running new command, `true/false`;
* `THEFUCK_WAIT_COMMAND` &ndash; max amount of time in seconds for getting previous command output;
* `THEFUCK_NO_COLORS` &ndash; disable colored output, `true/false`;
* `THEFUCK_PRIORITY` &ndash; priority of the rules, like `no_command=9999:apt_get=100`,
rule with lower `priority` will be matched first;
* `THEFUCK_DEBUG` &ndash; enables debug output, `true/false`.

For example:

```bash
export THEFUCK_RULES='sudo:no_command'
export THEFUCK_REQUIRE_CONFIRMATION='true'
export THEFUCK_WAIT_COMMAND=10
export THEFUCK_NO_COLORS='false'
export THEFUCK_PRIORITY='no_command=9999:apt_get=100'
```

## Developing

Install `The Fuck` for development:

```bash
pip install -r requirements.txt
python setup.py develop
```

Run unit tests:

```bash
py.test
```

Run unit and functional tests (requires docker):

```bash
FUNCTIONAL=true py.test
```

For sending package to pypi:

```bash
sudo apt-get install pandoc
./release.py
```

## License MIT
Project License can be found [here](LICENSE.md).
