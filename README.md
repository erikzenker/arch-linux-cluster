

# Arch Linux Cluster

Using arch linux distro to build a full cluster system.

## Installing the Base System

* Use antergos minimal image with base setup

* Install base software packages
  - base
  - base-devel
  - emacs-nox
  - git
  - pacaur


* Basic setup
  - Set hostname in `/etc/hostname`


## Installing SSH Server

* Install `openssh` package: `# pacman -S openssh`
* Start ssh daemon: `# systemctl enable sshd.service`
* Login: `ssh -p 22 User@HOSTNAME`

* Login node reachable from outside
* Compute nodes only reachable from login node

## Installing Network Filesystem

## Installing Batch System

## Installing Module System / Adding Further Software
### Using Nix
* Install nix `yaourt -S nix-multiuser`
  - `# mkdir -p /etc/nix`
  - `# touch /etc/nix/nix.conf`
  - `# echo "build-users-group = nixbld" > /etc/nix/nix.conf`
  - `# systemctl enable --now nix-daemon.socket` (restart shell necessary)
  - `# nix-channel --add https://nixos.org/channels/nixpkgs-unstable`
  - `# nix-channel --update`
  - `export CURL_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt`
  - Add `~/.nix-profile/bin` to `$PATH`

* Usage nix
  - Install packages: `nix-env -i PACKAGE_NAME`
  - Uninstall packages: `nix-env -e PACKAGE_NAME`
  - Search packages: `nix-env -qaP | grep PACKAGE_NAME`
  - Switch profile: `nix-env --switch-profile /nix/var/nix/profiles/my-profile`
  - create new profile: `cp -r OLD_PROFILE_PATH NEW_PROFILE_PATH`
  - List profiles: `ls /nix/var/nix/profiles/per-user/$USER`
  - List generations: `nix-env --list-generations`
  - Remove generations: `nix-env --delete-generations`
  - Switch generation: `nix-env -G GENERATION`
  - Switch to previous generaion: `nix-env --rollback`
  - List packages of current generation: `nix-env -q`

* Q&A:
  - Install nix-packets as non-root user?
    - Remove: `~/.nix-profile`
    - Run: `https://gist.github.com/erikzenker/807e9a39706e2ca1312ee052eaeaae22`
  - How to provide some kind of profile per user?
    - Provide a profiles folder: `~/profiles/`
    - Use nix file `my_profile.nix` and `nix-shell`
    - Set packages `nix-env --set PACKAGES`
  - Why takes cmake the gcc compiler from the overall default profile?
  - Cmake: the c compiler is not able to compile a simple test program
    - clang works / gcc currently not
### Using Spack
* Install spack: `git clone https://github.com/llnl/spack.git`
* Use bash: `bash`

* Usage spack
  - Install packages: `spack install PACKAGE_NAME@VERSION_NUMBER`
  - Use a particular compiler: `spack install PACKAGE_NAME@VERSION_NUMBER %COMPILER_NAME@COMPILER_VERSION`
    - to install with root `export FORCE_UNSAFE_CONFIGURE=1`
  - Show compilers: `spack compilers`  
  - Uninstall packages: `spack uninstall PACKAGE_NAME`
  - List installed packages: `spack find`
  - Search packages: `spack list PACKAGE_NAME`
  - List package versions: `spack versions PACKAGE_NAME`
  - Print package info: `spack info PACKAGE_NAME`
  - Switch prefix: `spack bootstrap NEW_PREFIX`
  
* Usage with environmental modules
  - Install the env-modules package: `pacaur -S env-modules`
  - Source init script for the particular shell: `source /etc/modules/init/bash`
  - Setup spack env for bash: `./share/spack/setup-env.sh`
  - List avail modules: `module avail`
  - Load module: `module load MODULE_NAME`
  - Unload module: `module unload MODULE_NAME`
  - List loaded modules: `module list`
  
* Known issues:
  - gcc 7.3.0/6.4.0 etc. might not be compilable by clang, or gcc 8.2.0
  
  
## Maintainance

* Refresh keys: `# pacman-key --refresh-keys`
* Update packets: `# pacman -Syu`

## Automatation of Node Installation

## Useful Links

* [Gentoo HPC Guide](https://wiki.gentoo.org/wiki/High_Performance_Computing_on_Gentoo)
* [Slurm](https://wiki.archlinux.org/index.php/Slurm)
* [Nix Package Manager Howto](https://nixos.org/nixos/manual/index.html#sec-ad-hoc-packages)
* [Environmental Modules](http://www.admin-magazine.com/HPC/Articles/Environment-Modules)
*  [Lmod: Environmental Modules Alternative](http://www.admin-magazine.com/HPC/Articles/Lmod-Alternative-Environment-Modules)
