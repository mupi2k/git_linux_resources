# git_linux_resources
linux resources like bashrc for sharing among multiple hosts

To use this resource:

1) create a location to clone the repo:
```mkdir ~/git_resources && cd ~/git_resources ```

2) clone this repo:
```git clone https://github.com/mupi2k/git_linux_resources.git .```


3) to use the resources here for ssh config, add the following to the TOP of your ~/.ssh/config:

```Include ~/git_resources/ssh/config```

4) to use included resources for .bashrc, add the contents of bashrc_template to your ~/.bashrc.
Ideally, that should be put at the TOP of your bashrc.  At a minimum, you will need:

```
# Paths.  Set at least $GIT_PATH to wherever you cloned the git linux resource repo to.
GIT_PATH="/home/$USER/git_resources"

if [ -f  $GIT_PATH/bash/bashrc ]; then
        . $GIT_PATH/bash/bashrc
fi

```

Of course if you used a location other than git_resources to clone to, you would need to update the locations in step 3 and 4.

By making this a separate directory under your home directory, although you lose the convienince of simply directly cloning your .bashrc, you also *gain* the ability to not worry about whatever else might be in your home directory, such as a ~/.ssh


