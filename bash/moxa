#!/bin/sh

# to make use of this file, be sure to check out ../readme.md
#
#  This file also expects VivintSolar/sentinel-scripts repo to be installed at $SENTINEL_PATH

# ovpn() and ovpns() will establish a connection to the ovpn server from the
#   jump box.  check_ip() should prevent a connection when one already exists.
#   if screens() doesn't show you an existing screen with an OVPN/OVPNS title, see
#        if someone else has the connection open.

OVPN_SUBNET=192.168.255
OVPNS_SUBNET=192.168.16

function check_ip()  {
    if [ -z $1 ]; then
        echo "Usage: check_ovpn [device]"
    else
        case "$@" in
            "-?")
                echo "Usage: check_ovpn [device]"
                ;;
            *)
                ip_command=$(jump /usr/sbin/ip a)
                for device in $@ ; do
                    echo "$ip_command" | awk -v device=$device '/inet/ {if ( $NF ~ device) print $2} '
                done
            ;;
        esac
    fi
}

function ovpn () {
    if [ -z $1 ]; then
        #echo "Usage: ovpn [destination/command]"
        if [ -n $DEBUG ]; then
            echo "running:  screen -S OVPN -t \"PROD\" -D -R sudo openvpn sentinel-prod.ovpn"
        fi
        CONN=$(check_ip tun{0,1} | awk -v net=$OVPN_SUBNET '{if ($0 ~ net) print $0; else print "none" }')
        if ! [ "$CONN" = "none" ]; then
            echo "Already connected to prod OVPN; aborting!"
            echo "Use screens() instead to attach to an existing OVPN screen session"
        else
            jump screen -S OVPN -t "PROD" -D -R sudo openvpn sentinel-prod.ovpn
        fi
    elif [ "$1" = "-?" ]; then
        echo "Usage: ovpn"
    fi
}

function ovpns () {
    if [ -z $1 ]; then
        #echo "Usage: jump_ovpns [destination/command]"
        if [ -n $DEBUG ]; then
            echo "running: screen -S OVPNS -t "STAGE" -D -R sudo openvpn sentinel-stage.ovpn"
        fi
        CONN=$(check_ip tun{0,1} | awk -v net=$OVPNS_SUBNET '{if ($0 ~ net) print $0; else print "none" }')
        if ! [ "$CONN" = "none" ]; then
            echo "Already connected to stage OVPN; aborting!"
            echo "Use screens() instead to attach to an existing OVPN screen session"
        else
            jump screen -S OVPNS -t "STAGE" -D -R sudo openvpn sentinel-stage.ovpn
        fi
    elif [ "$1" = "-?" ]; then
        echo "Usage: ovpns"
    fi
}

function moxa () {
    if [ -z $1 ]; then
        #echo "Usage: moxa [-s] [serial]"
        if [ -n $DEBUG ]; then
            echo "running: jump screen -S \"MOXATOOL\" -t \"TOOL\" -D -R $SENTINEL_PATH/moxatool.py"
        fi
        jump "cd $SENTINEL_PATH; screen -S MOXATOOL -t \"MOXATOOL\" -D -R ./moxatool.py"
    elif [ "$1" = "-s" ]; then
        shift
        if [ -z $1 ]; then
            jump "cd $SENTINEL_PATH; screen -S MOXA-STAGE -t \"MOXA-STAGE\" -D -R ./moxatool.py -s"
        else
            jump "cd $SENTINEL_PATH; screen -S STG-$1 -t \"STG-$1\" -D -R ./moxatool.py -s $1"
        fi
    elif [ "$1" = "-?" ]; then
          echo "Usage: jump ovpns"
    else
        jump "cd $SENTINEL_PATH; screen -S $1 -t $1 -D -R ./moxatool.py $1"
    fi
}

function new_moxa () {
    if [ -z $1 ]; then
        #echo "Usage: moxa [-s] [serial]"
        if [ -n $DEBUG ]; then
            echo "running: jump screen -S \"MOXATOOL\" -t \"TOOL\" $SENTINEL_PATH/moxatool.py"
        fi
        jump "cd $SENTINEL_PATH; screen -S MOXATOOL -t "MOXATOOL" $SENTINEL_PATH/moxatool.py"
    elif [ "$1" = "-s" ]; then
        shift
        if [ -z $1 ]; then
            jump "cd $SENTINEL_PATH; screen -S MOXA-STAGE -t "MOXA-STAGE" $SENTINEL_PATH/moxatool.py -s"
        else
            jump "cd $SENTINEL_PATH; screen -S STG-$1 -t "STG-$1" $SENTINEL_PATH/moxatool.py -s $1"
        fi
    elif [ "$1" = "-?" ]; then
          echo "Usage: jump ovpns"
    else
        jump "cd $SENTINEL_PATH; screen -S $1 -t $1  $SENTINEL_PATH/moxatool.py $1"
    fi
}
