# Reverse Engineer your .bash_profile

## Learning Goals

- Recognize what bash commands do
- Feel comfortable changing your dotfiles

## Introduction

Over time, you will adapt your tool configuration to your needs. Steadily, you'll make the most common parts of your workflow faster and faster. To start this positive feedback loop, you need to have comfort reading and changing your configuration.

**dotfiles** are files whose names are prefixed with a `.` - on many systems, that hides them from the system viewer (so you won't see the `.learn` file when you open a lab directory in the file explorer). Often, they configure programs that run. Other names you'll hear for the same fuzzy set of files are 'profile' and 'rc' ([run command](https://en.wikipedia.org/wiki/Run_commands)) files.

For instance, your `.bash_profile` file configures the `bash` program that runs in your terminal. bash runs your `.bash_profile` code whenever you start your terminal.

> Note: There's also a `.bashrc` file - see [.bash_profile vs .bashrc](http://www.joshstaiger.org/archives/2005/07/bash_profile_vs.html) for more on the difference.

## Exercise

- Open up your `~/.bash_profile`
- Mark each line with a comment, either explaining how the line works, or noting that you don't understand it yet
- Go back through the lines that you don't understand. For each one, take apart the syntax to figure out what it's doing.

## Bonus: aliases

bash has a few ways to define behavior. It has a `function` keyword, which works like javascript's `function` (the syntax is even similar!).

**aliases** are a slightly cheaper way to give a name to some behavior. Try it out in the terminal:

```sh
$ alias ha="echo 'hello aliases'"
$ ha
hello aliases
```

This alias only lasts as long as the terminal is open. If you want to always have your aliases around, you need to load them when your profile loads - perhaps in your `.bash_profile`!

Or, if you want to keep things uncluttered, you can create a new file `~/.bash_aliases` and keep all your aliases there. You'll need to add the following to your profile to load your aliases on start:

```sh
source ~/.bash_aliases
```

Now, you can also add a function to your `.bash_profile` that lets you add aliases.

```sh
# add an alias
# usage: `$ add_alias gb git branch`
function add_alias ()
{
    local cmd=$1;
    shift;
    local rest="$@";
    echo "alias $cmd=\"$rest\"" >> ~/.bash_aliases;
    source ~/.bash_aliases
}
```

Now you can type `add_alias co git checkout` and it will create a new shortcut for you. Some other favorites:

```sh
alias ga='git add'
alias gb='git branch'
alias gs='git status'
alias lf='learn --fail-fast'
```

You can see your current list of aliases by typing `alias` without any arguments. To see the definition of any bash function, you can use `type [name of function]` (e.g. `type add_alias` will show you the `add_alias` function).

> Challenge: see if you can write a bash function `add_export` that adds a new `export NAME=value` to a `.bash_exports` file.
