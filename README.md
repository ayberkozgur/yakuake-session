yakuaketwo-session - A script to create new yakuaketwo sessions from command-line.<br />
Copyright 2010-2013 Jesús Torres <aplatanado@gulic.org>

## What is yakuaketwo-session?

yakuaketwo-session is a Bash script that allows to create new sessions in yakuaketwo
terminal emulator from command line. I made it mainly to get a better
integration of yakuaketwo in KDE desktop environment. For example, thanks to it
yakuaketwo can replace Konsole in "Open terminal here" action in Dolphin or we
can setup a menu similar to Konsole Profiles widget but using yakuaketwo instead
of Konsole.

## Bugs & known issues

 * Bug [#1177823](http://bugs.launchpad.net/ubuntu/+source/qt4-x11/+bug/1177823)
breaks the command `qdbus` in Kubuntu 13.04/13.10. It can be fixed installing
`qt4-default` package.

## Installation

Clone this repository.

```
git clone https://github.com/aplatanado/yakuaketwo-session.git
```

Copy the yakuaketwo-session script to `~/bin`, `/usr/bin` or some other directory
in `$PATH` variable, if we want to avoid indicating the path of the script when
invoked. For example, on Ubuntu:

```
sudo cp yakuaketwo-session /usr/bin
```

## Usage

To invoke yakuaketwo-session:

```
$ yakuaketwo-session
```

Without arguments, yakuaketwo-session creates a new session in the currently
running yakuaketwo terminal emulator. 

The option `-e` allows to indicate a command to execute in the new session.

```
$ yakuaketwo-session -e ls
```

The argument `-t` sets the title for the new tab.

```
$ yakuaketwo-session -t "Title"
```

The session working directory is changed to the directory where yakuaketwo-session
was called, before execute the command. If we want to launch the command from
user's home directory then we would use the option `-h`.

```
$ yakuaketwo-session -h -e ls
```

If the command requires some arguments, they are taken from non-option
arguments passed to yakuaketwo-session. That means that if some arguments for the
command begin with `-`, they must passed to yakuaketwo-session after `--`.

```
$ yakuaketwo-session -h -e ssh -- -X user@example.com
```

Another useful option is `--workdir`. It allows to change the working directory
before execute the command.

```
$ yakuaketwo-session --workdir /tmp -e ls
```

yakuaketwo-session has many other options that were shown in help.

```
$ yakuaketwo-session --help

Usage: yakuaketwo-session [options] [args]

Options:
  --help                    Show help about options.
  -h, --homedir             Set the working directory of the new tab to the user's home.
  -w, --workdir <dir>       Set the working directory of the new tab to 'dir'
  --hold, --noclose         Do not close the session automatically when the command ends.
  -p <property=value>       Change the value of a profile property (only for KDE 4).
  -e <cmd>                  Command to execute.
  -q                        Do not open yakuaketwo window.
  -t <title>                Set the title of the new tab

Arguments:
  args                      Arguments passed to command.
```

## Action in Dolphin

Dolphin provides the action "Open terminal here" that opens a Konsole terminal
emulator in the specified folder. This behavior can be changed to use yakuaketwo
instead of Konsole coping `konsolehere.desktop` into KDE Service Menus. 

```
cp ServiceMenus/konsolehere.desktop ~/.kde/share/kde4/services/ServiceMenus/
```

If we do not want to change the behavior of "Open terminal here", then copy
`yakuaketwohere.desktop` instead to add the new action "Open yakuaketwo here" to
Dolphin.

```
cp ServiceMenus/yakuaketwohere.desktop ~/.kde/share/kde4/services/ServiceMenus/ 
```

## Quick Access Menu

Konsole Profiles is a Plasma widget that allows to open a new terminal window,
configured according to a select profile, and automatically execute a command
in it. We can get something similar but for yakuaketwo using the QuickAccess
widget. We only have to make a directory and setup a QuickAccess widget
instance to use it as origin (I also like to disable the browsing). Then we
add some "Link to Application" to that directory, such that each one use
yakuaketwo-session to create a new yakuaketwo session and to execute the command
that we want.

The file `examples/username@example.com.desktop` contains an example that launch
a ssh client in a new yakuaketwo session.


-- Jesús Torres <aplatanado@gulic.org>
