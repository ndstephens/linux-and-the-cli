# Package Management

- You need to install packages as root (can use `sudo`).
- Be aware that each Linux distro has its own package management tools.
  - Debian has `dpkg`. Because Ubuntu is based on Debian it also has `dpkg` installed and available to use.
  - `APT` (advanced packaging tool) is based on `dpkg` and available to all in the Debian family of distros
  - Red Hat had `RPM`, Red Hat Package Manager
  - Similar to how `APT` is on top of `dpkg`, `YUM` is on top of `RPM` to make it easier to use. `DNF` is the next generation of `YUM`
  - Arch has `Pacman`
  - Alpine has `APK`

## APT

### `apt-get`

- `apt-get` is older than `apt`. `apt-get` is a swiss army knife of `apt` and has a lot of flexibility and power to do different things.
- It also pairs wth `apt-cache` to accomplish some other tasks as well.
- Some folks got frustrated that `apt-get` was a bit difficult to use so they built a layer on top of it to be more user friendly...`apt`.

### `apt`

- `apt` is a tool that allows you to download new packages via `apt install <package>`. This will go out and fetch the package from the `apt` registry and install it.
- **_NOTE:_** Can install `aptitude` for a nice `apt` package management "UI" (`sudo apt install aptitude`)
- An example:

```sh
node -e "console.log('hi')" # this will fail, Node.js is not installed
apt search nodejs # search the registry for all packages with "nodejs" in their name or description
apt show nodejs # show details of the specific package called "nodejs"
sudo apt install nodejs
node -e "console.log('hi')" # now it works b/c Node.js was installed
```

- Some commands worth knowing:

```sh
sudo apt autoremove # will remove unused dependencies
sudo apt update # updates the list of available packages apt uses (does NOT actually update the packages on your computer)
apt list # everything installed
apt list --upgradable # everything with an update available
sudo apt upgrade # updates all your packages to their latest available versions
sudo apt upgrade <package> # update that package to its latest available version
sudo apt full-upgrade # basically autoremove and upgrade together
```

> Standard practice to run `update` before `upgrade`

## APT Browse

- A web browser for the contents of Debian (and Ubuntu) packages.
- [Website link](https://www.apt-browse.org/)
