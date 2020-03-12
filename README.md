# PackageDownloaders
Download packages with all of their dependencies for several different OSes, to enable an offline installation. Allows for configuration of hosts without connection to the internet.
Currently supported OSes:
* Ubuntu (.debs)
* FreeBSD (.txz)


# How to Use

## Ubuntu
```bash
sudo python get_deps_ubu.py <package_name>
```
where <package_name> is the same one you would use for apt. This script will use apt to download a package and all of its dependencies, organize them into directories and create an _installer.sh_ file that once you run will install everything in the right order.
If you want to get this working for different versions of Ubuntu, replace the sources in _/etc/apt/sources.list_ to the sources of your desired version and execute
```bash
sudo apt-get update
```
Then the script will download for that version of Ubuntu. You'll probably want to correct the sources back (and run update again) for apt to work normally.

Required packages (can be installed with apt):
* apt-rdepends
* python2.7
* python-regex

The script automatically downloads for x64. If you want x86, remove the comment in line 125.

## FreeBSD
```bash
sudo python get_deps_fbsd <package_name> <fbsd_version> <architecture>
```
where <package_name> is the exact name of the package you want to download, <fbsd_version> is the base version you want to work with and <architecture> is "x86:64" or "i386". To find the exact package name you can use the function _search_archives()_ in _fbsd_helper.py_.
The script creates a folder with the package and all of its dependencies, and to install everything automatically simply run
```bash
pkg add <package_name.txz>
```
Sometimes this will not be enough, and you will have to solve some compatability issues or go run the make file in the _ports_ directory of your desired package; but for most cases this will work out of the box.