# git_linux_resources
linux resources like bashrc for sharing among multiple hosts

To use this resource:

1) create a location to clone the repo:
```mkdir ~/git_resources && cd ~/git_resources ```

2) clone this repo:
```git clone https://github.com/mupi2k/git_linux_resources.git```


3) to use the resources here for ssh config, add the following to the TOP of your ~/.ssh/config:

```Include ~/git_resources/ssh/config```

4) to use included resources for .bashrc, add the following to your .bashrc:

```
if [ -f  ~/git_resources/bash/bashrc ]; then
        . ~/git_resources/bash/bashrc
fi
```

Of course if you used a location other than git_resources to clone to, you would need to update the locations in step 3 and 4.

By making this a separate directory under your home directory, although you lose the convienince of simply directly cloning your .bashrc, you also *gain* the ability to not worry about whatever else might be in your home directory, such as a ~/.ssh

There's a hard-coded reference to `~/git_resources` in `bash/bashrc` that you will want to edit if you don't like the git_resources path:
``` 
if [ -f ~/git_resources/bash/bash_aliases ]; then
    . ~/git_resouraces/bash/bash_aliases
fi
```
Because of the -f if clause, it won't break things, but the bash_aliases won't work.  If a future version breaks things into a more modular approach, then it will become more important, but at that point, a simple environment variable can carry the path through.
