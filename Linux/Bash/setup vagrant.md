---
Name: setup vagrant
Platform: Linux
tags:
  - Resources
---
Script to automate a bit setting up Vagrant VM boxes.

Example usage: `setup_vagrant.sh -n ubuntu/trusty64`

------

```bash
#!/usr/bin/env bash

VAGRANT_VM=""

usage() {  # Function: Print a help message.
  echo "Usage: $0 [ -n VAGRANT VM BOX NAME ]" 1>&2
  echo "---------------"
  echo "Example: $0 -n ubuntu/trusty64 (as according to https://app.vagrantup.com/ubuntu/boxes/trusty64)"

}

exit_abnormal() { # Function: Exit with error.
  usage
  echo "---------------"
  echo "Exiting!"
  exit 1
}

# Check if args were inputted

while getopts "n:h" opt
do
        case ${opt} in
        n)
                echo "Vagrant box name: ${OPTARG}"
                VAGRANT_VM="${OPTARG}"
                ;;
        h)
                echo "---------------"
                exit_abnormal
                ;;
        esac
done

# Check if supplied arguments are empty or not

if [[ -z "$VAGRANT_VM" ]]
then
        echo "[!] Not all required arugments were supplied"
        echo "---------------"
        exit_abnormal
        exit
fi

echo "[*] Setting up vagrant box"

DIR=${VAGRANT_VM//[\/]/_}

mkdir "$DIR" && cd "$DIR" && {
    vagrant init "$VAGRANT_VM"
    vagrant up
    vagrant suspend
}

```