- [Git Homepage](#git-homepage)
- [Installation](#installation)
  - [On macOS](#on-macos)
  - [On Windows](#on-windows)
  - [GitHub Desktop GUI Client](#github-desktop-gui-client)
  - [Git version Check](#git-version-check)
- [Git Configuration](#git-configuration)
- [Info Commands](#info-commands)
  - [git status](#git-status)
  - [git log](#git-log)
  - [git show](#git-show)
    - [Git-show options](#git-show-options)
    - [Pretty formats for Git-show](#pretty-formats-for-git-show)
    - [Examples of Git-show](#examples-of-git-show)
- [Setting up a repository](#setting-up-a-repository)
  - [git init](#git-init)
  - [git clone](#git-clone)
    - [Cloning to a specific folder](#cloning-to-a-specific-folder)
    - [Cloning a specific tag](#cloning-a-specific-tag)
    - [Shallow clone](#shallow-clone)
- [Saving changes](#saving-changes)
  - [git add](#git-add)
    - [Common options](#common-options)
    - [Examples](#examples)
  - [git commit](#git-commit)
    - [Common options](#common-options-1)
    - [Examples](#examples-1)
    - [How to update (amend) a commit](#how-to-update-amend-a-commit)
  - [.gitignore](#gitignore)
    - [Personal Git ignore rules](#personal-git-ignore-rules)
    - [Global Git ignore rules](#global-git-ignore-rules)
    - [Ignoring a previously committed file](#ignoring-a-previously-committed-file)
    - [Committing an ignored file](#committing-an-ignored-file)
- [Undoing Changes](#undoing-changes)
  - [git clean](#git-clean)
  - [git revert](#git-revert)
  - [git reset](#git-reset)
  - [git rm](#git-rm)
- [Branches](#branches)
- [Synchronize changes](#synchronize-changes)
- [git push](#git-push)


# Git Homepage

[https://git-scm.com/downloads](https://git-scm.com/downloads)

# Installation

## On macOS

macOS by default comes with `git` and is part of the operating system. You **DO NOT** want to un-install it.

If you want a different version, install it using brew using below command:

    $ brew install git

Homebrew (brew) will take care of all dependencies and configure the latest Git version, however there is still a chance it will find a setting it cannot resolve automatically, so read what Homebrew says at the end.

> _For optional GUI application_
>
>       $ brew install git-gui

## On Windows

Using `winget` tool:

    winget install --id Git.Git -e --source winget

> Links to Standalone or Portable installer can be found at [https://git-scm.com/downloads/win](https://git-scm.com/downloads/win).

## GitHub Desktop GUI Client

[https://desktop.github.com/download/](https://desktop.github.com/download/)

## Git version Check

Run below command to check installed version:

    $ git --version

# Git Configuration

| **Command** | **Description** |
| :-- | :-- |
| `git config --global user.name "[name]"` | Sets the name you want attached to your commit transactions |
| `git config --global user.email "[email address]"` | Sets the email you want attached to your commit transactions |
| `git config --global color.ui auto` | Enables helpful colorization of command line output |
| `$ git config --global core.excludesFile ~/.gitignore_global` | Set global `.gitignore` file.<br/>Be sure to create `.~/gitignore_global` file before executing this command. |

# Info Commands

## git status

The `git status` command displays the state of the working directory and the staging area. It lets you see which changes have been staged, which haven’t, and which files aren’t being tracked by Git. Status output does not show you any information regarding the committed project history. For this, you need to use `git log`.

## git log

The `git log` command displays committed snapshots. It lets you list the project history, filter it, and search for specific changes. While `git status` lets you inspect the working directory and the staging area, `git log` only operates on the committed history.

Log output can be customized in several ways, from simply filtering commits to displaying them in a completely user-defined format. Some of the most common configurations of `git log` are presented below.

* Display the entire commit history using the default formatting. If the output takes up more than one screen, you can use Space to scroll and q to exit.

        $ git log

* Limit the number of commits by . For example, git log -n 3 will display only 3 commits. Condense each commit to a single line. This is useful for getting a high-level overview of the project history.

        $ git log -n <limit>

* Along with the ordinary git log information, include which files were altered and the relative number of lines that were added or deleted from each of them.

        $ git log --oneline
        $ git log --stat

* Display the patch representing each commit. This shows the full diff of each commit, which is the most detailed view you can have of your project history.

        $ git log -p

* Search for commits by a particular author. The ＜pattern＞ argument can be a plain string or a regular expression.

        $ git log --author="<pattern>"

* Search for commits with a commit message that matches ＜pattern＞, which can be a plain string or a regular expression.

        $ git log --grep="<pattern>"

* Show only commits that occur between < since > and < until >. Both arguments can be either a commit ID, a branch name, HEAD, or any other kind of revision reference.

        $ git log <since>..<until>

* Only display commits that include the specified file. This is an easy way to see the history of a particular file.

        $ git log <file>

* A few useful options to consider. The --graph flag that will draw a text based graph of the commits on the left hand side of the commit messages. --decorate adds the names of branches or tags of the commits that are shown. --oneline shows the commit information on a single line making it easier to browse through commits at-a-glance.

        $ git log --graph --decorate --oneline

## git show

`git show` is a command line utility that is used to view expanded details on Git objects such as blobs, trees, tags, and commits. `git show` has specific behavior per object type.

Tags show the tag message and other objects included in the tag. Trees show the names and content of objects in a tree. Blobs show the direct content of the blob. Commits show a commit log message and a diff output of the changes in the commit.

Git objects are all accessed by references. By default, `git show` acts against the HEAD reference. The HEAD reference always points to the last commit of the current branch. Therefore, you can use `git show` to display the log message and diff output of the latest commit.

### Git-show options

* **`＜object＞…`**

    A reference to an object or a list of objects may be passed to examine those specific objects. If no explicit objects are passed, `git-show` defaults to the HEAD reference.

* **`--pretty[=＜format＞]`**

    The pretty option takes a secondary format value that can be one of: `oneline, short, medium, full, fuller, email, raw,` and `format:＜string＞`. If omitted, the format defaults to `medium`. Each format option is a different template for how Git formats the show output. The ＜code＞oneline＜/code＞ option can be very helpful for showing a list of commits

* **`--abbrev-commit`**

    This option shortens the length of output commit IDs. Commit IDs are 40 characters long and can be hard to view on narrow terminal screens. This option combined with `--pretty=oneline` can produce a highly succinct `git log` output.

* **`--no-abbrev-commit`**

    Always Show the full 40 character commit ID. This will ignore --`abbrev-commit` and any other options that abbreviate commit IDs like the `--oneline format`

* **`--oneline`**

    This is a shortcut for using the expanded command `--pretty=oneline --abbrev-commit`

* **`--encoding[=＜encoding＞]`**

    Character encoding on Git log messages defaults to UTF-8. The encoding option can change to a different character encoding output. This is useful if you are working with Git in an environment with different character encoding, like an Asian language terminal.

* **`＞--expand-tabs=＜n＞ --expand-tabs --no-expand-tabs`**

    These options replace tab characters with spaces in the log message output. The `n` value can be set to configure how many space characters the tabs expand to. Without an explicit n value tabs will expand to 8 spaces. `--no-expand-tabs` is equivalent to `n=0`

* **`--notes=＜ref＞ --no-notes`**

    Git has a note system that enables arbitrary ‘note’ metadata to be attached to objects. This data can be hidden or filtered when using `git-show`. 

* **`--show-signature`**

    This option will validate the commit is signed with an encrypted signature by passing it to a gpg subcommand.

### Pretty formats for Git-show

The `--pretty` option discussed above accepts several secondary options to massage the format of `git-show` output. These secondary options are listed below with example template

*   **oneline**

    `＜sha1> ＜title line>`

    Oneline attempts to compact as much info into a single line as possible

*   **short**

    `commit ＜sha1＞ Author: ＜author＞ ＜title line＞`

*   **medium**

    `commit ＜sha1＞ Author: ＜author＞ Date: ＜author date＞ ＜title line＞ ＜full commit message＞`

*   **full**

    `commit ＜sha1＞ Author: ＜author＞ Commit: ＜committer＞ ＜title line＞ ＜full commit message＞`

*   **fuller**

    `commit ＜sha1＞ Author: ＜author＞ AuthorDate: ＜author date＞ Commit: ＜committer＞ CommitDate: ＜committer date＞ ＜title line＞ ＜full commit message＞`

*   **email**

    `From ＜sha1＞ ＜date＞ From: ＜author＞ Date: ＜author date＞ Subject: [PATCH] ＜title line＞ ＜full commit message＞`

*   **raw**

    **raw** format ignores other direct formatting options passed to `git-show` and outputs the commit exactly as stored in the object. Raw will disregard `--abrev` and `--no-abbrev` and always show the parent commits.

*   **format:**

    format enables the specification of a custom output format. It works similar to the C language’s `printf` command. The `--pretty=format` option takes a secondary value of a template string. The template has access to placeholder variables that will be filled with data from the commit object. These placeholders are listed below:

    | Placeholder | Description |
    | :-: | :-- |
    | _%H_ | commit hash |
    | _%h_ | abbreviated commit hash |
    | _%T_ | tree hash |
    | _%t_ | abbreviated tree hash |
    | _%P_ | parent hashes |
    | _%p_ | abbreviated parent hashes |
    | _%an_ | author name |
    | _%aN_ | author name |
    | _%ae_ | author email |
    | _%aE_ | author email |
    | _%ad_ | author date (format respects --date= option) |
    | _%aD_ | author date, RFC2822 style |
    | _%ar_ | author date, relative |
    | _%at_ | author date, UNIX timestamp |
    | _%ai_ | author date, ISO 8601 format |
    | _%cn_ | committer name |
    | _%cN_ | committer name |
    | _%ce_ | committer email |
    | _%cE_ | committer email |
    | _%cd_ | committer date |
    | _%cD_ | committer date, RFC2822 style |
    | _%cr_ | committer date, relative |
    | _%ct_ | committer date, UNIX timestamp |
    | _%ci_ | committer date, ISO 8601 format |
    | _%d_ | ref names, like the --decorate option of git-log(1) |
    | _%e_ | encoding |
    | _%s_ | subject |
    | _%f_ | sanitized subject line, suitable for a filename |
    | _%b_ | body |
    | _%N_ | commit notes |
    | _%gD_ | reflog selector, e.g., refs/stash@{1} |
    | _%gd_ | shortened reflog selector, e.g., stash@{1} |
    | _%gs_ | reflog subject |
    | _%Cred_ | switch color to red |
    | _%Cgreen_ | switch color to green |
    | _%Cblue_ | switch color to blue |
    | _%Creset_ | reset color |
    | _%C(...)_ | color specification, as described in color.branch.\* config option |
    | _%m_ | left, right or boundary mark |
    | _%n_ | newline |
    | _%%_ | a raw % |
    | _%x00_ | print a byte from a hex code |
    | _%w(\[\[,\[,\]\]\])_ | switch line wrapping, like the -w option of git-shortlog |

### Examples of Git-show

    $ git show --pretty="" --name-only bd61ad98

This will list all the files that were touched in a commit

    $ git show REVISION:path/to/file

This will show a specific version of a file. Replace the `REVISON` with a Git sha.

    $ git show v2.0.0 6ef002d74cbbc099e1063728cab14ef1fc49c783

This will show the v2.0.0 tag and also commit at `6ef002d74cbbc099e1063728cab14ef1fc49c783`

    $ git show commitA...commitD

This will output all commits in the range from `commitA` to `commit D`

# Setting up a repository

## git init

    $ git init

The `git init` command creates a new Git repository. It can be used to convert an existing, unversioned project to a Git repository or initialize a new, empty repository. Most other Git commands are not available outside of an initialized repository, so this is usually the first command you'll run in a new project.

Executing `git init` creates a `.git` subdirectory in the current working directory, which contains all of the necessary Git metadata for the new repository. This metadata includes subdirectories for objects, refs, and template files. A HEAD file is also created which points to the currently checked out commit.

If you've already run `git init` on a project directory and it contains a `.git` subdirectory, you can safely run `git init` again on the same project directory. It will not override an existing `.git` configuration.

## git clone

    $ git clone [url]

`git clone` is primarily used to point to an existing repo and make a clone or copy of that repo at in a new directory, at another location. The original repository can be located on the local filesystem or on remote machine accessible supported protocols. The `git clone` command copies an existing Git repository. This is sort of like SVN checkout, except the “working copy” is a full-fledged Git repository—it has its own history, manages its own files, and is a completely isolated environment from the original repository.

As a convenience, cloning automatically creates a remote connection called "origin" pointing back to the original repository. This makes it very easy to interact with a central repository. This automatic connection is established by creating Git refs to the remote branch heads under `refs/remotes/origin` and by initializing `remote.origin.url` and `remote.origin.fetch` configuration variables.

The example below demonstrates how to obtain a local copy of a central repository stored on a server accessible at `example.com` using the SSH username john:

    $ git clone ssh://john@example.com/path/to/my-project.git
    $ cd my-project
    # Start working on the project

### Cloning to a specific folder

    git clone <repo> <directory>

Clone the repository located at `＜repo＞` into the folder called `~＜directory＞!` on the local machine.

### Cloning a specific tag

    git clone --branch <tag> <repo>

Clone the repository located at `＜repo＞` and only clone the ref for `＜tag＞`.

### Shallow clone

    git clone -depth=1 <repo>

Clone the repository located at `＜repo＞` and only clone the  history of commits specified by the option depth=1. In this example a clone of `＜repo＞` is made and only the most recent commit is included in the new cloned Repo. Shallow cloning is most useful when working with repos that have an extensive commit history. An extensive commit history may cause scaling problems such as disk space usage limits and long wait times when cloning. A Shallow clone can help alleviate these scaling issues.

# Saving changes

## git add

    $ git add .
    $ git commit -m "[descriptive message]"

The commands: `git add`, `git status`, and `git commit` are all used in combination to save a snapshot of a Git project's current state.

The `git add` command adds a change in the working directory to the staging area. It tells Git that you want to include updates to a particular file in the next commit. However, `git add` doesn't really affect the repository in any significant way—changes are not actually recorded until you run `git commit`.

In conjunction with these commands, you'll also need `git status` to view the state of the working directory and the staging area.

### Common options

    git add <file>

Stage all changes in `<file>` for the next commit.

    git add <directory>

Stage all changes in `<directory>` for the next commit.

    git add -p

Begin an interactive staging session that lets you choose portions of a file to add to the next commit. This will present you with a chunk of changes and prompt you for a command. Use `y` to stage the chunk, `n` to ignore the chunk, `s` to split it into smaller chunks, `e` to manually edit the chunk, and `q` to exit.

### Examples

To create an initial commit of the current directory, use the following two commands:

    $ git add .
    $ git commit

Once you’ve got your project up-and-running, new files can be added by passing the path to `git add`:

    $ git add hello.py
    $ git commit

The above commands can also be used to record changes to existing files. Again, Git doesn’t differentiate between staging changes in new files vs. changes in files that have already been added to the repository.

## git commit

The `git commit` command captures a snapshot of the project's currently staged changes. Committed snapshots can be thought of as “safe” versions of a project—Git will never change them unless you explicitly ask it to.

Prior to the execution of `git commit`, the `git add` command is used to promote or 'stage' changes to the project that will be stored in a commit. These two commands `git commit` and `git add` are two of the most frequently used.

### Common options

    $ git commit

Commit the staged snapshot. This will launch a text editor prompting you for a commit message. After you’ve entered a message, save the file and close the editor to create the actual commit.

    $ git commit -a

Commit a snapshot of all changes in the working directory. This only includes modifications to tracked files (those that have been added with `git add` at some point in their history).

    $ git commit -m "commit message"

A shortcut command that immediately creates a commit with a passed commit message. By default, `git commit` will open up the locally configured text editor, and prompt for a commit message to be entered. Passing the `-m` option will forgo the text editor prompt in-favor of an inline message.

    $ git commit -am "commit message"

A power user shortcut command that combines the `-a` and `-m` options. This combination immediately creates a commit of all the staged changes and takes an inline commit message.

    $ git commit --amend

This option adds another level of functionality to the commit command. Passing this option will modify the last commit. Instead of creating a new commit, staged changes will be added to the previous commit. This command will open up the system's configured text editor and prompt to change the previously specified commit message.

### Examples

The following example assumes you’ve edited some content in a file called `hello.py` on the current branch, and are ready to commit it to the project history. First, you need to stage the file with `git add`, then you can commit the staged snapshot.

    $ git add hello.py

This command will add `hello.py` to the Git staging area. We can examine the result of this action by using the `git status` command.

    $ git status
    On branch main
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
       new file: hello.py

The green output new file: `hello.py` indicates that `hello.py` will be saved with the next commit. From the commit is created by executing:

    $ git commit

This will open a text editor (customizable via `git config`) asking for a commit log message, along with a list of what’s being committed:

    # Please enter the commit message for your changes. Lines starting
    # with '#' will be ignored, and an empty message aborts the commit.
    # On branch main
    # Changes to be committed:
    # (use "git reset HEAD ..." to unstage)
    #
    #modified: hello.py

Git doesn't require commit messages to follow any specific formatting constraints, but the canonical format is to summarize the entire commit on the first line in less than 50 characters, leave a blank line, then a detailed explanation of what’s been changed. For example:

    Change the message displayed by hello.py

    - Update the sayHello() function to output the user's name
    - Change the sayGoodbye() function to a friendlier message

It is a common practice to use the first line of the commit message as a subject line, similar to an email. The rest of the log message is considered the body and used to communicate details of the commit change set. Note that many developers also like to use the present tense in their commit messages. This makes them read more like actions on the repository, which makes many of the history-rewriting operations more intuitive.

### How to update (amend) a commit

To continue with the `hello.py` example above. Let's make further updates to `hello.py` and execute the following:

    $ git add hello.py
    $ git commit --amend

This will once again, open up the configured text editor. This time, however, it will be pre-filled with the commit message we previously entered. This indicates that we are not creating a new commit, but editing the last.

## .gitignore

Sometimes it may be a good idea to exclude files from being tracked with Git. This is typically done in a special file named `.gitignore`. You can find helpful templates for `.gitignore` files at [https://github.com/github/gitignore](https://github.com/github/gitignore).

Git ignore rules are usually defined in a `.gitignore` file at the root of your repository. However, you can choose to define multiple `.gitignore` files in different directories in your repository. Each pattern in a particular `.gitignore` file is tested relative to the directory containing that file. However the convention, and simplest approach, is to define a single `.gitignore` file in the root. As your `.gitignore` file is checked in, it is versioned like any other file in your repository and shared with your teammates when you push. Typically you should only include patterns in `.gitignore` that will benefit other users of the repository.

`.gitignore` uses [globbing patterns](http://linux.die.net/man/7/glob) to match against file names. You can construct your patterns using various symbols:

| **Pattern** | **Example matches** | **\*Explanation** |
| :-- | :-- | :-- |
| `**/logs` | `logs/debug.log`<br/>`logs/monday/foo.bar`<br/>`build/logs/debug.log` | You can prepend a pattern with a double asterisk to match directories anywhere in the repository. |
| `**/logs/debug.log` | `logs/debug.log`<br/>`build/logs/debug.log`<br/>_but not_<br/>`logs/build/debug.log` | You can also use a double asterisk to match files based on their name and the name of their parent directory. |
| `*.log` | `debug.log`<br/>`foo.log`<br/><br/>`.log`<br/><br/>`logs/debug.log` | An asterisk is a wildcard that matches zero or more characters. |
| `*.log`<br/>`!important.log` | `debug.log`<br/>_but not_<br/>`logs/debug.log` | Prepending an exclamation mark to a pattern negates it. If a file matches a pattern, but _also_ matches a negating pattern defined later in the file, it will not be ignored. |
| `/debug.log` | `debug.log`<br/>_but not_<br/>`logs/debug.log` | Patterns defined after a negating pattern will re-ignore any previously negated files. |
| `debug.log` | `debug.log`<br/>`logs/debug.log` | Prepending a slash matches files only in the repository root. |
| `debug?.log` | `debug0.log`<br/>`debugg.log`<br/>_but not_<br/>`debug10.log` | A question mark matches exactly one character. |
| `debug[0-9].log` | `debug0.log`<br/>`debug1.log`<br/>_but not_<br/>`debug10.log` | Square brackets can also be used to match a single character from a specified range. |
| `debug[01].log` | `debug0.log`<br/>`debug1.log`<br/>_but not_<br/>`debug2.log`<br/>`debug01.log` | Square brackets match a single character form the specified set. |
| `debug[!01].log` | `debug2.log`<br/>_but not_<br/>`debug0.log`<br/>`debug1.log`<br/>`debug01.log` | An exclamation mark can be used to match any character except one from the specified set. |
| `debug[a-z].log` | `debuga.log`<br/>`debugb.log`<br/>_but not_<br/>`debug1.log` | Ranges can be numeric or alphabetic. |
| `logs` | `logs`<br/>`logs/debug.log`<br/>`logs/latest/foo.bar`<br/>`build/logs`<br/>`build/logs/debug.log`<br/> | If you don't append a slash, the pattern will match both files and the contents of directories with that name. In the example matches on the left, both directories and files named _logs_ are ignored |
| `logs/` | `logs/debug.log`<br/>`logs/latest/foo.bar`<br/>`build/logs/foo.bar`<br/>`build/logs/latest/debug.log` | Appending a slash indicates the pattern is a directory. The entire contents of any directory in the repository matching that name – including all of its files and subdirectories – will be ignored |
| `logs/`<br/>`!logs/important.log` | `logs/debug.log`<br/>`logs/important.log` | Wait a minute! Shouldn't `logs/important.log`be negated in the example on the left<br/>Nope! Due to a performance-related quirk in Git, you can not negate a file that is ignored due to a pattern matching a directory |
| `logs/**/debug.log` | `logs/debug.log`<br/>`logs/monday/debug.log`<br/>`logs/monday/pm/debug.log` | A double asterisk matches zero or more directories. |
| `logs/*day/debug.log` | `logs/monday/debug.log`<br/>`logs/tuesday/debug.log`<br/>_but not_<br/>`logs/latest/debug.log` | Wildcards can be used in directory names as well. |
| `logs/debug.log` | `logs/debug.log`<br/>_but not_<br/>`debug.log`<br/>`build/logs/debug.log` | Patterns specifying a file in a particular directory are relative to the repository root. (You can prepend a slash if you  |like, but it doesn't do anything special.) |

> \*_these explanations assume your .gitignore file is in the top level directory of your repository, as is the convention. If your repository has multiple .gitignore files, simply mentally replace "repository root" with "directory containing the .gitignore file" (and consider unifying them, for the sanity of your team)._

In addition to these characters, you can use `#` to include comments in your `.gitignore` file:

    # ignore all logs
    *.log

You can use `\` to escape `.gitignore` pattern characters if you have files or directories containing them:

    # ignore the file literally named foo[01].txt
    foo\[01\].txt

### Personal Git ignore rules

You can also define personal ignore patterns for a particular repository in a special file at `.git/info/exclude`. These are not versioned, and not distributed with your repository, so it's an appropriate place to include patterns that will likely only benefit you. For example if you have a custom logging setup, or special development tools that produce files in your repository's working directory, you could consider adding them to `.git/info/exclude` to prevent them from being accidentally committed to your repository.

### Global Git ignore rules

In addition, you can define global Git ignore patterns for all repositories on your local system by setting the Git `core.excludesFile` property. You'll have to create this file yourself. If you're unsure where to put your global `.gitignore` file, your home directory isn't a bad choice (and makes it easy to find later). Once you've created the file, you'll need to configure its location with `git config`:

You don’t have to name it `.gitignore_global`. You could name it `.gitignore` as well. I appended `_global` so future me will remember what the file is used for.

    $ touch ~/.gitignore_global
    $ git config --global core.excludesFile ~/.gitignore_global

For Windows, navigate to the root folder of your user profile usually at `C:\Users\[myusername]\`and create a `.gitignore_global` file. Then run,

    git config --global core.excludesfile "%USERPROFILE%\.gitignore_global"

If using Windows PowerShell then run,

    git config --global core.excludesfile "$Env:USERPROFILE\.gitignore_global"

To verify the global exclude file config, run:

    git config --global core.excludesfile

The output should be the full path to your file.

You should be careful what patterns you choose to globally ignore, as different file types are relevant for different projects. Special operating system files (e.g. `.DS_Store` and `thumbs.db`) or temporary files created by some developer tools are typical candidates for ignoring globally.

My current `.gitignore_global` file in macOS is below:

    # General
    .DS_Store
    .AppleDouble
    .LSOverride

    # Icon must end with two \r
    Icon


    # Thumbnails
    ._*

    # Files that might appear in the root of a volume
    .DocumentRevisions-V100
    .fseventsd
    .Spotlight-V100
    .TemporaryItems
    .Trashes
    .VolumeIcon.icns
    .com.apple.timemachine.donotpresent

    # Directories potentially created on remote AFP share
    .AppleDB
    .AppleDesktop
    Network Trash Folder
    Temporary Items
    .apdisk

My current `.gitignore_global` file in macOS is below:

    # Windows thumbnail cache files
    Thumbs.db
    Thumbs.db:encryptable
    ehthumbs.db
    ehthumbs_vista.db

    # Dump file
    *.stackdump

    # Folder config file
    [Dd]esktop.ini

    # Recycle Bin used on file shares
    $RECYCLE.BIN/

    # Windows Installer files
    *.cab
    *.msi
    *.msix
    *.msm
    *.msp

    # Windows shortcuts
    *.lnk

### Ignoring a previously committed file

If you want to ignore a file that you've committed in the past, you'll need to delete the file from your repository and then add a `.gitignore` rule for it. Using the `--cached` option with `git rm` means that the file will be deleted from your repository, but will remain in your working directory as an ignored file.

    $ echo debug.log >> .gitignore
      
    $ git rm --cached debug.log
    rm 'debug.log'
      
    $ git commit -m "Start ignoring debug.log"

You can omit the `--cached` option if you want to delete the file from both the repository and your local file system.

### Committing an ignored file

It is possible to force an ignored file to be committed to the repository using the `-f` (or `--force`) option with `git add`:

    $ cat .gitignore
    *.log
      
    $ git add -f debug.log
      
    $ git commit -m "Force adding debug.log"

You might consider doing this if you have a general pattern (like `*.log`) defined, but you want to commit a specific file. However a better solution is to define an exception to the general rule:

    $ echo !debug.log >> .gitignore
      
    $ cat .gitignore
    *.log
    !debug.log
      
    $ git add debug.log
      
    $ git commit -m "Adding debug.log"

This approach is more obvious, and less confusing, for your teammates.

# Undoing Changes

## git clean

## git revert

## git reset

https://www.atlassian.com/git/tutorials/undoing-changes/git-reset

## git rm


# Branches

Branches are an important part of working with Git. Any commits you make will be made on the branch you're currently "checked out" to. Use `git status` to see which branch that is.

* Create new branch

    ```bash
    $ git branch [branch-name]
    ```

* Switch to the specified branch and updates the working directory

    ```bash
    $ git checkout [branch-name]
    ```

* Deletes the specified branch

    ```bash
    $ git branch -d [branch-name]
    ```

* Combine the specified branch’s history into the current branch. This is usually done in pull requests, but is an important Git operation.

    ```bash
    $ git merge [branch]
    ```

# Synchronize changes

Synchronize your local repository with the remote repository on GitHub.com

* Download all history from the remote tracking branches

    ```bash
    $ git fetch
    ```

* Combine remote tracking branch into current local branch

    ```bash
    $ git merge
    ```

* Upload all local branch commits to GitHub

    ```bash
    $ git push
    ```

* Updates your current local working branch with all new commits from the corresponding remote branch on GitHub. `git pull` is a combination of `git fetch` and `git merge`

    ```bash
    $ git pull
    ```

# git push

https://www.atlassian.com/git/tutorials/syncing/git-push

