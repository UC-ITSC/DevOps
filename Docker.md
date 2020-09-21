# Install Docker on a new server

## SUSE 12 (Official repo) [Official Documentation](https://documentation.suse.com/sles/12-SP4/single-html/SLES-dockerquick/index.html#cha-docker-installation)

1. `sudo SUSEConnect -p sle-module-containers/12/x86_64 -r ''`
2. `sudo zypper refresh`
3. `sudo zypper install docker`
4. `Use systemctl commands to start docker`
5. `sudo usermod -aG docker $USER`
6. `Exit the server and re-ssh the server`

Docker is now installed and ready to use

For older servers, you may have to downgrade docker until it starts working.

1. List versions: `zypper se -v docker`
2. `sudo zypper in -f docker-version-tag-here` (e.x. `sudo zypper in -f docker-17.09.1_ce-98.12.1`)