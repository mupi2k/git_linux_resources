#!/bin/sh

###############################################################################
##  git_linux_resources/bash/functions
##     functions for bashrc
##

# see ../readme.md

function title {
    echo -en "\033]2;$1\007"
    SCREEN_TITLE=$1
}

function jump() {
    if [ -z $1 ]; then
        #echo "Usage: jump [command]"
        if ! [ -z $DEBUG ]; then
            echo "running: /usr/bin/ssh -t -A -Y -p $BASTION_PORT  $BASTION_USERNAME@$BASTION_SERVER"
        fi
        /usr/bin/ssh -t -A -Y -p $BASTION_PORT $BASTION_USERNAME@$BASTION_SERVER
    elif [ "$1" = "-?" ]; then
        echo "Usage: jump [command]"
    else
        CMD=$1  #if we made it this far, there's at least a $1
        title "JUMP-$CMD"
        shift
        if [ -z "$1" ]; then
            if ! [ -z $DEBUG ]; then
                echo "running: /usr/bin/ssh -t -A -Y -p $BASTION_PORT  $BASTION_USERNAME@$DESKTOP $CMD"
            fi
            /usr/bin/ssh -t -A -Y -p $BASTION_PORT $BASTION_USERNAME@$BASTION_SERVER $CMD
        else
            if ! [ -z $DEBUG ]; then
                echo "running: /usr/bin/ssh -t -A -Y -p $BASTION_PORT $BASTION_USERNAME@$DESKTOP  $CMD \"$@\""
            fi
        /usr/bin/ssh -t -A -Y -p $BASTION_PORT $BASTION_USERNAME@$BASTION_SERVER $CMD "$@"
        fi
    fi
}

function jj() {
    if [ -z $1 ]; then
        echo "Usage: jj ssh-destination [ssh-command]"
    else
        DEST=$1  #we know if we are here, we have at least a $1
        shift
        if [ -z "$@" ]; then
            if ! [ -z $DEBUG ]; then
                echo "running: jump jscreen $DEST"
            fi
            jump jscreen $DEST
        else
            if ! [ -z $DEBUG ]; then
                echo "running: jump jscreen $DEST $@"
            fi
            jump jscreen $DEST $@
       fi
    fi
}
