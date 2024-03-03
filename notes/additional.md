#### Install systemctl on ubuntu
```shell
# install systemd
apt install systemd

# check the PATH environment variable
echo $PATH

# add the directory to the PATH environment variable
export PATH=$PATH:/usr/bin/systemctl

# make systemctl command executable
chmod +x /usr/bin/systemctl

# check if your system is running a systemd-based init system, output must `systemd`
ps -p 1 -o comm=
```