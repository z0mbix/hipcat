hipcat
======

This is something we've been using at work for several years to easily send messages to hipchat, and finally found time to open source it. We use it for many things. Some ideas:

- Send notifications from deploy/build scripts
- Send installation notifications from RPM/DEB post-install scripts
- Send messages from automation scripts (backups etc.)
- Send the output from cron jobs
- Send messages when files/directories change using [incrond](http://incron.aiken.cz)

This is very simple and the only dependency is 'curl'.

## Setup

You need to set you hipchat API token as an environment variable:

    export HIPCAT_TOKEN=1234567890


## Usage

Pipe message to hipcat, specifying the room:

    $ echo "What the deuce?" | hipcat -r 123456

Pass message directly to hipcat, also specifying the room:

    $ hipcat -r 123456 -m "Giggity..."

If you export HIPCAT_ROOMS (one or more space separated), you don't need to use the -r option:

    $ export HIPCAT_ROOMS="1234 5678"
    $ date | hipcat

Run 'hipcat' with no options to see full usage details:

    $ hipcat
    Usage: /usr/bin/hipcat -r [room_id(s)] -m [message -c [colour] -f [from] -n -h
    At least one room ID and a message (including stdin) is required.
    Use -f to change who the message is from
    Use -n to notify room
    Use -h to send an HTML message
    Use -c to set the message colour (yellow|red|green|purple|gray|random)
    Your hipchat token should be specified by exporting HIPCAT_TOKEN

## TODO

- Read token and rooms from a config file?