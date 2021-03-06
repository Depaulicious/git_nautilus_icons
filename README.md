# git-nautilus-icons

Use Git? Use Nautilus? Why not have Nautilus give you info about your repos?

`git-nautilus-icons` overlays emblems saying whether files are modified,
added, untracked etc, with a high level of detail showing the exact status of
the file including both staged and unstaged changes separately. It marks git
repos as such and displays icons on them showing whether they have changed
files, unpushed commits, etc.

## Installation

`git-nautilus-icons` requires `python-nautilus`, the python `pathlib` library
and the python `enum34` library. On Ubuntu these are installable with: `sudo
apt-get install python-pathlib python-nautilus python-enum34`

to install `git-nautilus-icons`, put the single python file `git-nautilus-
icons.py` in `~/.local/share/nautilus-python/extensions`, and put the icons
folder `hicolor` in `~/.icons/`. These directories might not exist, in which
case create them. You can use the following commands to do so:

```bash
cd /tmp
git clone https://github.com/chrisjbillington/git_nautilus_icons
cd git_nautilus_icons/
mkdir -p ~/.icons
cp -r icons/hicolor ~/.icons
mkdir -p ~/.local/share/nautilus-python/extensions
cp git-nautilus-icons.py ~/.local/share/nautilus-python/extensions
```

Then restart Nautilus with `killall nautilus` and the plugin will be loaded next time
a Nautilus window is opened.

To uninstall, simply delete `git-nautilus-icons.py` and the `hicolor` icons
folder.

## Icon key

Here is what each possible file status looks like, as well as a few examples
of what repositories may look like. Folders and repositories are marked with
the status of their contents, with the 'worst' status in the index and work
tree shown (not necessarily from the same file). For files deleted from the
work tree, their status will only be visible via their parent directory, so
this is how they are shown below. Repos are also marked with whether or not
they are ahead of remote.

![alt tag](key.png)

## Blacklisting

You can blacklist repositories, to tell `git-nautilus-icons` not to check
their status. This could be useful in the case of an extremely large
repository where calling `git status` is slow and so the extension slows down
browsing in Nautilus. Git is pretty fast, so I haven't seen this, but I hear
such massive repos exist. Nautilus can also be pretty slow rendering those
icons, so even if your repo is not that big, you may wish to blacklist one if
you have a large number of files in a single folder and it slows Nautilus down
enough.

To blacklist a repository, add its full path to the list `blacklist` at the
top of `git-nautilus-icons.py`.

Close Nautilus with `killall nautilus` after changing the blacklist, it
will take effect when Nautilus it is restarted.

## Notes

Icons are updated every time you browse to a directory, but whilst in a
directory, Nautilus doesn't ask the extension for new icons unless it sees a
file change on disk. Tap F5 in Nautilius to force a refresh.
