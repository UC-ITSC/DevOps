# Install Docker on a new server (SUSE 12)

**NOTE:** This version of Docker only works on SLES 12 SP3 and higher. `cat /etc/os-release` to find the server version

1. `sudo zypper addrepo https://download.opensuse.org/repositories/Virtualization:containers/openSUSE_Tumbleweed_and_d_l_g/Virtualization:containers.repo`
1. `sudo zypper refresh`
1. `sudo zypper install docker`
1. `sudo systemctl enable docker`
1. `sudo systemctl start docker`
1. `sudo usermod -a -G docker $USER`
1. Send `exit` command and re-ssh the server

Docker is now installed and ready to use

(You may need to update libseccomp2 on SP3 systems `https://software.opensuse.org/download/package?package=libseccomp2&project=security`)

# FAQ

* ERROR: IPv4 forwarding is disabled. Networking will not work.
    1. `sudo vi /etc/sysctl.conf`
    1. Change `net.ipv4.ip_forward = 0` to `net.ipv4.ip_forward = 1` and save changes
    1. `sudo systemctl restart network`
    1. `sudo systemctl restart docker`
    1. This should be fixed

# Install docker-compose

1. <https://docs.docker.com/compose/install/>

# Nuke docker installation and start over

__WARNING__ This action cannot be undone!

1. `sudo zypper remove docker`
2. `sudo su`
3. `cd /var/lib/docker/btrfs/subvolumes`
4. `ls | xargs btrfs subvolume delete`
5. `cd && rm-rf /var/lib/docker`
6. Reinstall docker
