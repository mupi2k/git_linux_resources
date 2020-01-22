#!/bin/sh

###############################################################################
##  git_linux_resources/bash/screen
##     functions to use screen
##
##     requires bash/functions
# see ../readme.md

function screens() {
    /usr/bin/ssh -tAp $BASTION_PORT $BASTION_USERNAME@$BASTION_SERVER "screen -ls"
}

function jscreen() {
    if [ -z $1 ]
    then
        echo "Usage: jscreen ssh-destination [ssh-command]"
    else
        DEST=$1  #we know if we are here, we have at least a $1
	      SCREEN_TITLE=$DEST
        shift
        if [ -z "$1" ]; then
            if ! [ -z $DEBUG ]; then
                echo "running: screen -S $DEST -t $SCREEN_TITLE -D -R /usr/bin/ssh -t -A $DEST"
            fi
            screen -S $DEST -t $SCREEN_TITLE -D -R /usr/bin/ssh -t -A  $DEST
        else
            if ! [ -z $DEBUG ]; then
                echo "running screen -S $DEST -t $SCREEN_TITLE -D -R \"/usr/bin/ssh -t -A $DEST \"$@\""
            fi
            screen -S $DEST -t $SCREEN_TITLE -D -R "/usr/bin/ssh -t -A $DEST \"$@\""
        fi
    fi
}

function restore() {
    for i in $(screens | awk '/tached/ {print $1}' | cut -d. -f2)
    do
        echo restoring $i...
        terminator -e "jj $i"

    done

    }
