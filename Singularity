################################################################################
# Basic bootstrap definition to build CentOS 7 container from Docker container
################################################################################

BootStrap: docker
From: kaixhin/cuda-torch
 
################################################################################
# Copy any necessary files into the container
################################################################################
%files
#./etc/profile.d/z_container_prompt.sh  /etc/profile.d/z_container_prompt.sh
#./etc/profile.d/z_container_prompt.csh /etc/profile.d/z_container_prompt.csh
 
%post
################################################################################
# Make sure the umask is 0022
################################################################################
umask 0022

################################################################################
# Install additional login shells for users that need them
################################################################################
# yum -y install tcsh ksh zsh

################################################################################
# Install additional packages
################################################################################
# apt-get install vim
# apt-get install git

################################################################################
# Install torch and torch dependencies
################################################################################
# git clone https://github.com/torch/distro.git ~/torch --recursive
# cd ~/torch
# bash -y install-deps
# cd
# git clone https://github.com/deepmind/torch-hdf5
# sudo apt-get install libhdf5-serial-dev hdf5-tools
# luarocks make hdf5-0-0.rockspec LIBHDF5_LIBDIR="/usr/lib/x86_64-linux-gnu/"
# luarocks install qtlua

################################################################################
# Install PIP from EPEL and upgrade it to the latest version
################################################################################
# sudo apt-get -y install epel-release
# sudo apt-get -y install python3-pip python-pip
# sudo apt-get -y install python3-tk
# pip  install --upgrade pip
# pip3 install --upgrade pip
# pip  install --upgrade virtualenv

################################################################################
# Create directories to enable access to common HPCC mount points
################################################################################
# mkdir /boot
# mkdir /cvmfs
mkdir -p /mnt/home
mkdir -p /mnt/research
mkdir -p /mnt/dfs17
mkdir -p /mnt/ffs17
mkdir -p /mnt/local
mkdir -p /mnt/ls15
mkdir -p /opt/software

################################################################################
# Run the user's login shell, or a user specified command
################################################################################
%runscript
SHELL="$(getent passwd $USER | awk -F: '{print $NF}')"
SHELL=${SHELL:-/bin/bash}
if [[ "$@" == "" ]]; then 
  exec env -i TERM="$TERM" HOME="$HOME" $SHELL -l
else
  exec env -i TERM="$TERM" HOME="$HOME" $@
fi
