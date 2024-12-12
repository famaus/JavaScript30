- [Git Homepage](#git-homepage)
- [Installation](#installation)
  - [On macOS](#on-macos)
  - [On Windows](#on-windows)
  - [GitHub Desktop GUI Client](#github-desktop-gui-client)
  - [Git version Check](#git-version-check)
- [Git Configuration](#git-configuration)
  - [git config editor - core.editor](#git-config-editor---coreeditor)
  - [git alias](#git-alias)
    - [Example: Using aliases to create new Git commands](#example-using-aliases-to-create-new-git-commands)
- [Info Commands](#info-commands)
  - [git status](#git-status)
  - [git log](#git-log)
  - [git show](#git-show)
    - [Git-show options](#git-show-options)
    - [Pretty formats for Git-show](#pretty-formats-for-git-show)
    - [Examples of Git-show](#examples-of-git-show)
  - [git diff](#git-diff)
    - [Comparing files](#comparing-files)
    - [Comparing all changes](#comparing-all-changes)
    - [Comparing files between two different commits](#comparing-files-between-two-different-commits)
    - [Comparing two branches](#comparing-two-branches)
    - [Comparing files from two branches](#comparing-files-from-two-branches)
  - [git blame](#git-blame)
    - [Common options](#common-options)
    - [Git blame vs git log](#git-blame-vs-git-log)
- [Setting up a repository](#setting-up-a-repository)
  - [git init](#git-init)
  - [git clone](#git-clone)
    - [Cloning to a specific folder](#cloning-to-a-specific-folder)
    - [Cloning a specific tag](#cloning-a-specific-tag)
    - [Shallow clone](#shallow-clone)
- [Saving changes](#saving-changes)
  - [git add](#git-add)
    - [Common options](#common-options-1)
    - [Examples](#examples)
  - [git commit](#git-commit)
    - [Common options](#common-options-2)
    - [Examples](#examples-1)
    - [How to update (amend) a commit](#how-to-update-amend-a-commit)
  - [git tag](#git-tag)
    - [Creating a tag](#creating-a-tag)
    - [Annotated tags](#annotated-tags)
    - [Lightweight tags](#lightweight-tags)
    - [Listing tags](#listing-tags)
    - [Tagging old commits](#tagging-old-commits)
    - [ReTagging/Replacing old tags](#retaggingreplacing-old-tags)
    - [Sharing: Pushing tags to remote](#sharing-pushing-tags-to-remote)
    - [Checking out tags](#checking-out-tags)
    - [Deleting tags](#deleting-tags)
  - [.gitignore](#gitignore)
    - [Personal Git ignore rules](#personal-git-ignore-rules)
    - [Global Git ignore rules](#global-git-ignore-rules)
    - [Ignoring a previously committed file](#ignoring-a-previously-committed-file)
    - [Committing an ignored file](#committing-an-ignored-file)
    - [Debugging .gitignore files](#debugging-gitignore-files)
- [Undoing Changes](#undoing-changes)
  - [git clean](#git-clean)
    - [Common options and usage](#common-options-and-usage)
  - [git revert](#git-revert)
  - [git reset](#git-reset)
  - [git rm](#git-rm)
    - [Usage](#usage)
    - [How to undo git rm](#how-to-undo-git-rm)
    - [Why use git rm instead of rm](#why-use-git-rm-instead-of-rm)
    - [How to remove files no longer in the filesystem](#how-to-remove-files-no-longer-in-the-filesystem)
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

## git config editor - core.editor

Many Git commands will launch a text editor to prompt for further input. One of the most common use cases for `git config` is configuring which editor Git should use. Listed below is a table of popular editors and matching `git config` commands:

| **Editor** | **config command** |
| :-- | :-- |
| Atom | `$ git config --global core.editor "atom --wait"` |
| emacs | `$ git config --global core.editor "emacs"` |
| nano | `$ git config --global core.editor "nano -w"` |
| vim | `$ git config --global core.editor "vim"` |
| Sublime Text (Mac) | `$ git config --global core.editor "subl -n -w"` |
| Sublime Text (Win, 32-bit install) | `$ git config --global core.editor "'c:/program files (x86)/sublime text 3/sublimetext.exe' -w"` |
| Sublime Text (Win, 64-bit install) | `$ git config --global core.editor "'c:/program files/sublime text 3/sublimetext.exe' -w"` |
| Textmate | `$ git config --global core.editor "mate -w"` |

## git alias

Git aliases are a powerful workflow tool that create shortcuts to frequently used Git commands. Using Git aliases will make you a faster and more efficient developer. Aliases can be used to wrap a sequence of Git commands into new faux Git command. Git aliases are created through the use of the git config command which essentially modifies local or global Git config files.

To better understand Git aliases let us create some examples.

    $ git config --global alias.co checkout
    $ git config --global alias.br branch
    $ git config --global alias.ci commit
    $ git config --global alias.st status

On linux systems, the global config file is located in the User home directory at `/.gitconfig`.

    [alias]
    co = checkout
    br = branch
    ci = commit
    st = status

### Example: Using aliases to create new Git commands

A common Git pattern is to remove recently added files from the staging area. This is achieved by leveraging options to the `git reset` command. A new alias can be created to encapsulate this behavior and create a new alias-command-keyword which is easy to remember:

    $ git config --global alias.unstage 'reset HEAD --'

The preceding code example creates a new alias `unstage`. This now enables the invocation of `git unstage. git unstage` which will perform a reset on the staging area. This makes the following two commands equivalent.

    $ git unstage fileA
    $ git reset HEAD -- fileA

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

## git diff

`git diff` is a multi-use Git command that when executed runs a diff function on Git data sources. These data sources can be commits, branches, files and more. The `git diff` command is often used along with `git status` and `git log` to analyze the current state of a Git repo.

To understand this command, consider below example:

    $ git log --oneline
    460740c (HEAD -> master) reverting back to fourth
    0a4a799 restore to third change
    c922b14 fourth change
    efae9f8 third change
    335a181 second change
    1976f2d (tag: v1.0) first change
    8eca64f empty file

    $ git diff efae9f8 c922b14
    diff --git a/demo_file b/demo_file
    index ed585a5..d81c4f3 100644
    --- a/demo_file
    +++ b/demo_file
    @@ -1,3 +1,4 @@
    first change
    second change
    third change
   +fourth change

1\. Comparison input

    diff --git a/demo_file b/demo_file

This line displays the input sources of the diff. We can see that `a/demo_file` and `b/demo_file` have been passed to the diff.

2\. Meta data

    index ed585a5..d81c4f3 100644

This line displays some internal Git metadata. You will most likely not need this information. The numbers in this output correspond to Git object version hash identifiers.

3\. Markers for changes

    --- a/demo_file
    +++ b/demo_file

These lines are a legend that assigns symbols to each diff input source. In this case, changes from `a/demo_file` are marked with a `---` and the changes from `b/demo_file` are marked with the `+++` symbol.

4\. Diff chunks

The remaining diff output is a list of diff 'chunks'. A diff only displays the sections of the file that have changes. In our current example, we only have one chunk as we are working with a simple scenario. Chunks have their own granular output semantics.

    @@ -1,3 +1,4 @@
    first change
    second change
    third change
   +fourth change

The first line is the chunk header. Each chunk is prepended by a header enclosed within `@@` symbols. The content of the header is a summary of changes made to the file. In our simplified example, we have -1 +1 meaning line one had changes. In a more realistic diff, you would see a header like:

    @@ -34,6 +34,8 @@

In this header example, 6 lines have been extracted starting from line number 34. Additionally, 8 lines have been added starting at line number 34.

The remaining content of the diff chunk displays the recent changes. Each changed line is prepended with a `+` or `-` symbol indicating which version of the diff input the changes come from. As we previously discussed, `-` indicates changes from the `a/demo_file` and + indicates changes from `b/demo_file`.

### Comparing files

The `git diff` command can be passed an explicit file path option. When a file path is passed to `git diff` the diff operation will be scoped to the specified file. The below examples demonstrate this usage.

    $ git diff HEAD ./path/to/file

This example is scoped to `./path/to/file` when invoked, it will compare the specific changes in the working directory, against the index, showing the changes that are not staged yet. By default `git diff` will execute the comparison against `HEAD`. Omitting `HEAD` in the example above `git diff ./path/to/file` has the same effect.

    $ git diff --cached ./path/to/file

When `git diff` is invoked with the `--cached` option the diff will compare the staged changes with the local repository. The `--cached` option is synonymous with `--staged`.

### Comparing all changes

Invoking `git diff` without a file path will compare changes across the entire repository. The above, file specific examples, can be invoked without the `./path/to/file` argument and have the same output results across all files in the local repo.

### Comparing files between two different commits

`git diff` can be passed Git refs to commits to diff. Some example refs are, `HEAD`, tags, and branch names. Every commit in Git has a commit ID which you can get when you execute `GIT LOG`. You can also pass this commit ID to `git diff`.

    $ git log --pretty=oneline
    957fbc92b123030c389bf8b4b874522bdf2db72c add feature
    ce489262a1ee34340440e55a0b99ea6918e19e7a rename some classes
    6b539f280d8b0ec4874671bae9c6bed80b788006 refactor some code for feature
    646e7863348a427e1ed9163a9a96fa759112f102 add some copy to body

    $:> git diff 957fbc92b123030c389bf8b4b874522bdf2db72c ce489262a1ee34340440e55a0b99ea6918e19e7a

###  Comparing two branches

Branches are compared like all other ref inputs to `git diff`

    $ git diff branch1..other-feature-branch

This example introduces the dot operator. The two dots in this example indicate the diff input is the tips of both branches. The same effect happens if the dots are omitted and a space is used between the branches. Additionally, there is a three dot operator:

    $ git diff branch1...other-feature-branch

The three dot operator initiates the diff by changing the first input parameter `branch1`. It changes `branch1` into a ref of the shared common ancestor commit between the two diff inputs, the shared ancestor of `branch1` and other-feature-branch. The last parameter input parameter remains unchanged as the tip of other-feature-branch.

### Comparing files from two branches

To compare a specific file across branches, pass in the path of the file as the third argument to `git diff`

    $ git diff main new_branch ./diff_test.txt

## git blame

The high-level function of `git blame` is the display of author metadata attached to specific committed lines in a file. This is used to examine specific points of a file's history and get context as to who the last author was that modified the line. This is used to explore the history of specific code and answer questions about what, how, and why the code was added to a repository.

`git blame` only operates on individual files. A file-path is required for any useful output. The default execution of `git blame` will simply output the commands help menu. For this example, we will operate on sample README.MD file.

    $ git blame README.MD

Executing the above command will give us our first sample of blame output. Consider the following output is a subset of the full blame output of the README. Additionally, this output is static is reflective of the state of the repo at the time of this writing.

    $ git blame README.md
        82496ea3 (kevzettler     2018-02-28 13:37:02 -0800  1) # Git Blame example
        82496ea3 (kevzettler     2018-02-28 13:37:02 -0800  2)
        89feb84d (Albert So      2018-03-01 00:54:03 +0000  3) This repository is an example of a project with multiple contributors making commits.
        82496ea3 (kevzettler     2018-02-28 13:37:02 -0800  4)
        82496ea3 (kevzettler     2018-02-28 13:37:02 -0800  5) The repo use used elsewhere to demonstrate `git blame`
        82496ea3 (kevzettler     2018-02-28 13:37:02 -0800  6)
        89feb84d (Albert So      2018-03-01 00:54:03 +0000  7) Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod TEMPOR incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum
        89feb84d (Albert So      2018-03-01 00:54:03 +0000  8)
        eb06faed (Juni Mukherjee 2018-03-01 19:53:23 +0000  9) Annotates each line in the given file with information from the revision which last modified the line. Optionally, start annotating from the given revision.
        eb06faed (Juni Mukherjee 2018-03-01 19:53:23 +0000 10)
        548dabed (Juni Mukherjee 2018-03-01 19:55:15 +0000 11) Creating a line to support documentation needs for git blame.
        548dabed (Juni Mukherjee 2018-03-01 19:55:15 +0000 12)
        548dabed (Juni Mukherjee 2018-03-01 19:55:15 +0000 13) Also, it is important to have a few of these commits to clearly reflect the who, the what and the when. This will help Kev get good screenshots when he runs the git blame on this README.

This is a sample of the first 13 lines of the README.md file. To better understand this output lets break down a line. The following table displays the content of line 3 and the columns of the table indicate the column content.

| Id | Author | Timestamp | Line Number | Line Content |
| :-: | :-: | :-: | :-: | :-- |
| 89feb84d | Albert So | 2018-03-01 00:54:03 +0000 | 3 | This repository is an example of a project with multiple contributors making commits. |

If we review the blame output list, we can make some observations. There are three authors listed. In addition to the project's maintainer Kev Zettler, Albert So, and Juni Mukherjee are also listed. Authors are generally the most valuable part of `git blame` output. The timestamp column is also primarily helpful. What the change was is indicated by line content column.

### Common options

    $ git blame -L 1,5 README.md

The `-L` option will restrict the output to the requested line range. Here we have restricted the output to lines 1 through 5.

    $ git blame -e README.md

The `-e` option shows the authors email address instead of username.

    $ git blame -w README.md

The `-w` option ignores whitespace changes. If a previous author has modified the spacing of a file by switching from tabs to spaces or adding new lines this, unfortunately, obscures the output of `git blame` by showing these changes.

    $ git blame -M README.md

The `-M` option detects moved or copied lines within in the same file. This will report the original author of the lines instead of the last author that moved or copied the lines.

    $ git blame -C README.md

The `-C` option detects lines that were moved or copied from other files. This will report the original author of the lines instead of the last author that moved or copied the lines.

### Git blame vs git log

While `git blame` displays the last author that modified a line, often times you will want to know when a line was originally added. This can be cumbersome to achieve using `git blame`. It requires a combination of the `-w`, `-C`, and `-M` options. It can be far more convenient to use the `git log` command.

To list all original commits in-which a specific code piece was added or modified execute `git log` with the `-S` option. Append the `-S` option with the code you are looking for. Let's take one of the lines from the README output above to use as an example. Let us take the text "CSS3D and WebGL renderers" from Line 12 of the README output.

    $ git log -S"CSS3D and WebGL renderers." --pretty=format:'%h %an %ad %s'
    e339d3c85 Mario Schuettel Tue Oct 13 16:51:06 2015 +0200 reverted README.md to original content
    509c2cc35 Daniel Tue Sep 8 13:56:14 2015 +0200 Updated README
    cb20237cc Mr.doob Mon Dec 31 00:22:36 2012 +0100 Removed DOMRenderer. Now with the CSS3DRenderer it has become irrelevant.

This output shows us that content from the README was added or modified 3 times by 3 different authors. It was originally added in commit cb20237cc by Mr.doob. In this example, `git log` has also been prepended with the `--pretty-format` option. This option converts the default output format of `git log` into one that matches the format of `git log`.





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

## git tag

Tags are ref's that point to specific points in Git history. Tagging is generally used to capture a point in history that is used for a marked version release (i.e. v1.0.1).

A tag is like a branch that doesn’t change. Unlike branches, tags, after being created, have no further history of commits.

### Creating a tag

To create a new tag execute the following command:

    $ git tag <tagname>

Replace `<tagname>` with a semantic identifier to the state of the repo at the time the tag is being created. A common pattern is to use version numbers like `git tag v1.4`.

Git supports two different types of tags, annotated and lightweight tags. The previous example created a lightweight tag. Lightweight tags and Annotated tags differ in the amount of accompanying meta data they store. A best practice is to consider Annotated tags as public, and Lightweight tags as private. Annotated tags store extra meta data such as: the tagger name, email, and date. This is important data for a public release. Lightweight tags are essentially 'bookmarks' to a commit, they are just a name and a pointer to a commit, useful for creating quick links to relevant commits.

### Annotated tags

Annotated tags are stored as full objects in the Git database. To reiterate, They store extra meta data such as: the tagger name, email, and date. Similar to commits and commit messages Annotated tags have a tagging message. Additionally, for security, annotated tags can be signed and verified with GNU Privacy Guard (GPG). Suggested best practices for git tagging is to prefer annotated tags over lightweight so you can have all the associated meta-data.

    $ git tag -a v1.4

Executing this command will create a new annotated tag identified with `v1.4`. The command will then open up the configured default text editor to prompt for further meta data input.

    $ git tag -a v1.4 -m "my version 1.4"

Executing this command is similar to the previous invocation, however, this version of the command is passed the `-m` option and a message. This is a convenience method similar to `git commit -m` that will immediately create a new tag and forgo opening the local text editor in favor of saving the message passed in with the `-m` option.

### Lightweight tags

    $ git tag v1.4-lw

Executing this command creates a lightweight tag identified as `v1.4-lw.` Lightweight tags are created with the absence of the `-a`, `-s`, or `-m` options. Lightweight tags create a new tag checksum and store it in the `.git/` directory of the project's repo.

### Listing tags

To list stored tags in a repo execute the following:

    $ git tag

To refine the list of tags the `-l` option can be passed with a wild card expression:

    $ git tag -l *-rc*
    v0.10.0-rc1
    v0.11.0-rc1
    v0.12.0-rc1
    v0.13.0-rc1
    v0.13.0-rc2
    v0.14.0-rc1
    v0.9.0-rc1
    v15.0.0-rc.1
    v15.0.0-rc.2
    v15.4.0-rc.3

This previous example uses the `-l` option and a wildcard expression of `-rc` which returns a list of all tags marked with a `-rc` prefix, traditionally used to identify _release candidates_.

### Tagging old commits

The previous tagging examples have demonstrated operations on implicit commits. By default, `git tag` will create a tag on the commit that `HEAD` is referencing. Alternatively `git tag` can be passed as a ref to a specific commit. This will tag the passed commit instead of defaulting to `HEAD.` To gather a list of older commits execute the `git log` command.

    $ git log --oneline
    3b1d230 (HEAD -> master) fixed EOL
    460740c reverting back to fourth
    0a4a799 restore to third change
    f9ec630 Revert to "fourth change"
    2e5676f Revert to "fourth change"
    c922b14 fourth change
    efae9f8 third change
    335a181 second change
    1976f2d (tag: v1.0) first change
    8eca64f empty file

Executing `git log` will output a list of commits. In this example we will pick `second change` for the new tag. We will need to reference to the commit SHA hash to pass to Git:

    $ git tag -a v1.2 335a181

Executing the above `git tag` invocation will create a new annotated commit identified as `v1.2` for the commit we selected in the previous `git log` example.

### ReTagging/Replacing old tags

If you try to create a tag with the same identifier as an existing tag, Git will throw an error like:

    fatal: tag 'v0.4' already exists

Additionally if you try to tag an older commit with an existing tag identifier Git will throw the same error.

In the event that you must update an existing tag, the `-f FORCE` option must be used.

    $ git tag -a -f v1.4 15027957951b64cf874c3557a0f3547bd83b3ff6

Executing the above command will map the `15027957951b64cf874c3557a0f3547bd83b3ff6` commit to the `v1.4` tag identifier. It will override any existing content for the `v1.4` tag.

### Sharing: Pushing tags to remote

Sharing tags is similar to pushing branches. By default, `git push` will not push tags. Tags have to be explicitly passed to `git push`.

    $ git push origin v1.4
    Counting objects: 14, done.
    Delta compression using up to 8 threads.
    Compressing objects: 100% (12/12), done.
    Writing objects: 100% (14/14), 2.05 KiB | 0 bytes/s, done.
    Total 14 (delta 3), reused 0 (delta 0)
    To git@bitbucket.com:atlasbro/gittagdocs.git
     * [new tag]         v1.4 -> v1.4

To push multiple tags simultaneously pass the `--tags` option to `git push` command. When another user clones or pulls a repo they will receive the new tags.

### Checking out tags

You can view the state of a repo at a tag by using the [git checkout](https://www.atlassian.com/git/tutorials/using-branches/git-checkout) command.

    $ git checkout v1.4

The above command will checkout the `v1.4` tag. This puts the repo in a detached `HEAD` state. This means any changes made will not update the tag. They will create a new detached commit. This new detached commit will not be part of any branch and will only be reachable directly by the commits SHA hash. Therefore it is a best practice to create a new branch anytime you're making changes in a detached `HEAD` state.

### Deleting tags

Deleting tags is a straightforward operation. Passing the `-d` option and a tag identifier to `git tag` will delete the identified tag.

    $ git tag
    v1
    v2
    v3
    $ git tag -d v1
    $ git tag
    v2
    v3

In this example `git tag` is executed to display a list of tags showing v1, v2, v3, Then `git tag -d v1` is executed which deletes the v1 tag.

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

### Debugging .gitignore files

If you have complicated `.gitignore` patterns, or patterns spread over multiple `.gitignore` files, it can be difficult to track down why a particular file is being ignored. You can use the `git check-ignore` command with the `-v` (or `--verbose`) option to determine which pattern is causing a particular file to be ignored:

    $ git check-ignore -v debug.log
    .gitignore:3:*.log  debug.log

The output shows:

    <file containing the pattern> : <line number of the pattern> : <pattern>    <file name>

You can pass multiple file names to `git check-ignore` if you like, and the names themselves don't even have to correspond to files that exist in your repository.

# Undoing Changes

## git clean

Git clean can be considered complementary to other commands like git reset and git checkout. Whereas these other commands operate on files previously added to the Git tracking index, the git clean command operates on untracked files. Untracked files are files that have been created within your repo's working directory but have not yet been added to the repository's tracking index using the git add command.

### Common options and usage

    -n

The `-n` option will perform a “dry run” of git clean. This will show you which files are going to be removed without actually removing them. It is a best practice to always first perform a dry run of git clean.

    -f or --force

The force option initiates the actual deletion of untracked files from the current directory. Force is required unless the `clean.requireForce` configuration option is set to false. This will not remove untracked folders or files specified by `.gitignore`.

    -d include directories

The -d option tells git clean that you also want to remove any untracked directories, by default it will ignore directories.

    -x force removal of ignored files

A common software release pattern is to have a build or distribution directory that is not committed to the repositories tracking index. The build directory will contain ephemeral build artifacts that are generated from the committed source code. This build directory is usually added to the repositories `.gitignore` file. It can be convenient to also clean this directory with other untracked files. The `-x` option tells git clean to also include any ignored files. As with previous git clean invocations, it is a best practice to execute a 'dry run' first, before the final deletion. The `-x` option will act on all ignored files, not just project build specific ones. This could be unintended things like `.idea` IDE configuration files.

    git clean -xf

Like the `-d` option `-x` can be passed and composed with other options. This example demonstrates a combination with `-f` that will remove untracked files from the current directory as well as any files that Git usually ignores.

    -i interactive mode

git clean has an "interactive" mode that you can initiate by passing the -i option. The interactive mode will display a What now> prompt that requests a command to apply to the untracked files. The commands themselves are fairly self explanatory.

## git revert

The `git revert` command can be considered an 'undo' type command, however, it is not a traditional undo operation. Instead of removing the commit from the project history, it figures out how to invert the changes introduced by the commit and appends a new commit with the resulting inverse content. This prevents Git from losing history, which is important for the integrity of your revision history and for reliable collaboration.

Reverting should be used when you want to apply the inverse of a commit from your project history. This can be useful, for example, if you’re tracking down a bug and find that it was introduced by a single commit. Instead of manually going in, fixing it, and committing a new snapshot, you can use `git revert` to automatically do all of this for you.

Below are the steps to revert a commit:

    # Step 1: first check the commit history
    git log --oneline

    # Step 2: select the commit you want to revert
    git revert nd7hjd9

    # Step 3: Resolve  any conflicts that might arive
    # Edit the file(s) in your preferred editor to resolve conflicts
    # Then mark the resolved files
    git add [file]

    # in case of all files
    git add .

    # Step 4: Complete the revert commit
    git commit -m "Revert commit h7i8j9k to fix bug in feature Y"

    # Step 5: Push the revert commit to the remote repository
    git push origin master

## git reset

The `git reset` command is used to reset current HEAD to a specified state. It can modify the index and working directory depending on the options used. Here are the main types of reset:

1. **Soft Reset** (`git reset --soft <commit>`):

    This moves the HEAD pointer to a specified commit but leaves your working directory and staging area (index) unchanged. It's useful if you want to undo a commit but keep your changes staged.

        $ git reset --soft HEAD~1

     This undoes the last commit, keeping the changes staged.

2. **Mixed Reset** (`git reset --mixed <commit>`):

    This is the default mode. It moves the HEAD pointer and updates the index to match the specified commit, but it does not change the working directory. This unstages changes that were committed.

        $ git reset HEAD~1

    This undoes the last commit and unstages the changes, allowing you to modify them before committing again.

3. **Hard Reset** (`git reset --hard <commit>`):

    This resets the HEAD pointer, the index, and the working directory to the specified commit. It will discard all changes, so use this with caution.

    $ git reset --hard HEAD~1

    This completely removes the last commit and all changes associated with it.

4. **Resetting to a Specific Commit**:

    You can also reset to any specific commit by using its SHA.

    $ git reset --hard abc1234

    This resets the repository to the state of the commit with SHA `abc1234`.

Remember to always be careful when using `--hard` as it irreversibly deletes changes.

## git rm

The `git rm` command can be used to remove individual files or a collection of files. The primary function of `git rm` is to remove tracked files from the Git index. Additionally, `git rm` can be used to remove files from both the staging index and the working directory. There is no option to remove a file from only the working directory. The files being operated on must be identical to the files in the current `HEAD`. If there is a discrepancy between the `HEAD` version of a file and the staging index or working tree version, Git will block the removal. This block is a safety mechanism to prevent removal of in-progress changes.

### Usage

    <file>…​

Specifies the target files to remove. The option value can be an individual file, a space delimited list of files `file1 file2 file3`, or a wildcard file glob `(~./directory/*)`.

    -f
    --force

The `-f` option is used to override the safety check that Git makes to ensure that the files in `HEAD`  match the current content in the staging index and working directory.

    -n
    --dry-run

The "dry run" option is a safeguard that will execute the `git rm` command but not actually delete the files. Instead it will output which files it would have removed.

    -r

The `-r` option is shorthand for 'recursive'. When operating in recursive mode `git rm` will remove a target directory and all the contents of that directory.

    --

The separator option is used to explicitly distinguish between a list of file names and the arguments being passed to `git rm`. This is useful if some of the file names have syntax that might be mistaken for other options.

    --cached

The cached option specifies that the removal should happen only on the staging index. Working directory files will be left alone.

    --ignore-unmatch

This causes the command to exit with a 0 sigterm status even if no files matched. This is a Unix level status code. The code 0 indicates a successful invocation of the command. The `--ignore-unmatch` option can be helpful when using `git rm` as part of a greater shell script that needs to fail gracefully.

    -q
    --quiet

The quiet option hides the output of the `git rm` command. The command normally outputs one line for each file removed.

### How to undo git rm

Executing `git rm` is not a permanent update. The command will update the staging index and the working directory. These changes will not be persisted until a new commit is created and the changes are added to the commit history. This means that the changes here can be "undone" using common Git commands.

    git reset HEAD

A reset will revert the current staging index and working directory back to the `HEAD` commit. This will undo a `git rm`.

    git checkout .

A checkout will have the same effect and restore the latest version of a file from `HEAD`.

In the event that `git rm` was executed and a new commit was created which persist the removal, `git reflog` can be used to find a ref that is before the `git rm` execution.

### Why use git rm instead of rm

A Git repository will recognize when a regular shell `rm` command has been executed on a file it is tracking. It will update the working directory to reflect the removal. It will not update the staging index with the removal. An additional `git add` command will have to be executed on the removed file paths to add the changes to the staging index. The `git rm` command acts a shortcut in that it will update the working directory and the staging index with the removal.

### How to remove files no longer in the filesystem

As stated above in "Why use `git rm` instead of `rm`" , `git rm` is actually a convenience command that combines the standard shell `rm` and `git add` to remove a file from the working directory and promote that removal to the staging index. A repository can get into a cumbersome state in the event that several files have been removed using only the standard shell `rm` command.

If intentions are to record all the explicitly removed files as part of the next commit, `git commit -a` will add all the removal events to the staging index in preparation of the next commit.

If however, intentions are to persistently remove the files that were removed with the shell `rm`, use the following command:

    git diff --name-only --diff-filter=D -z | xargs -0 git rm --cached


This command will generate a list of the removed files from the working directory and pipe that list to `git rm --cached` which will update the staging index.

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

