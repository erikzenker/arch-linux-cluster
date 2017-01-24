

# Arch Linux Cluster

Using arch linux distro to build a full cluster system.

## Installing the Base System

* Use antergos minimal image with base setup

* Install base software packages
  * emacs-nox

* Basic setup
- Set hostname in `/etc/hostname`


## Installing SSH Server

* Install `openssh` package: `# pacman -S openssh`
* Start ssh daemon: `# systemctl enable sshd.service`

* Login node reachable from outside
* Compute nodes only reachable from login node

## Installing Network Filesystem

## Installing Batch System

## Installing Module System

* Install nix `yaourt -S nix-multiuser`
- `# mkdir -p /etc/nix`
- `# touch /etc/nix/nix.conf`
- `# echo "build-users-group = nixbld" > /etc/nix/nix.conf`
- `# systemctl enable --now nix-daemon.socket` (restart shell necessary)
- `# nix-channel --add https://nixos.org/channels/nixpkgs-unstable`
- `# nix-channel --update`
- `export CURL_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt`
- Add `~/.nix-profile/bin` to `$PATH`
- Install packages: `nix-env -i PACKAGE_NAME`
- Search packages: `nix-env -qaP | grep PACKAGE_NAME`
- Switch profile: `nix-env --switch-profile /nix/var/nix/profiles/my-profile`


## Automatation of Node Installation

## Useful Links

* [Gentoo HPC Guide](https://wiki.gentoo.org/wiki/High_Performance_Computing_on_Gentoo)
* [Slurm](https://wiki.archlinux.org/index.php/Slurm)
* [Nix Package Manager Howto](https://nixos.org/nixos/manual/index.html#sec-ad-hoc-packages)
