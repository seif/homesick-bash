Homesick castle bash
====================

This is a [homesick](https://github.com/technicalpickles/homesick) _castle_ for [bash](http://www.bash.org/).

* [Solarized](http://ethanschoonover.com/solarized) color scheme
* Tailored for Linux, Solaris, and MacOS. Preliminary support for SmartOS

Includes
--------

Includes are bash scripts that are sourced. First general scripts are sourced, then os specific, then distro specific, and finally hostname specific.

The order and locations of the files are:

1 ```~/.bashrc.os.d/common```
2 ```~/.bashrc.os.d/${BASHRC_OS}-common```
3 ```~/.bashrc.os.d/${BASHRC_OS}-${BASHRC_OS_DISTRO}```
4 ```~/.bashrc.${BASHRC_HOST_CONFIG}.d``` where BASHRC_HOST_CONFIG is the node name without the domain part.

The files included are, in the following order:

* ```colors```      -- *internal* create color tables

* ```main```        -- set ```COLOR_BG_IS``` to either ```DARK``` or ```LIGHT```, dpendening on whether the terminal BG is light or dark
* ```path```        -- Augement the path
* ```alias```       -- Define ```alias```es.
* ```exports```     -- Keep exports togehter

* ```bashprompt```  -- *internal* Set up the bashprompt

### Plugins
Plugins AKA other castles can hook into the sourcing lifecycle by provifing a file matching the glob ```~/.bashrc-plugin.*.d```. ```.bashrc``` will source the file ```plugin.conf``` according to the rules described above.


### Example

On the system ```home``` which is an Ubuntu system, while sourcing ```.bashrc``` the following ```alias``` files are sourced in the following order (if they exist):

1 ```~/.bashrc.os.d/common/alias```
2 ```~/.bashrc.os.d/linux-common/alias```
3 ```~/.bashrc.os.d/linux-debian/alias```
4 ```~/.bashrc.home.d/alias```

If a directory ```~/.bashrc-plugin.myplugin.d``` exists, then the following files would be sourced as well (if they exist):

1 ```~/.bashrc-plugin.myplugin.d/common/plugin.conf```
2 ```~/.bashrc-plugin.myplugin.d/linux-common/plugin.conf```
3 ```~/.bashrc-plugin.myplugin.d/linux-debian/plugin.conf```
4 ```~/.bashrc.home.d/myplugin.conf```


Variables
---------

### Common

* ```BASHRC_HOST_CONFIG``` -  The hostname used for host-specific configuration files. Defined in ```.bashrc```. *Exported*
* ```BASHRC_ALREADY_CONFIGURED``` - Has ```.bashrc``` already been sourced? Set to ```yes``` if so. Defined in ```.bashrc```.

### OS dependend

* ```BASHRC_OS``` -- The OS running. Values for BASHRC_OS are:
     * ```aix```     -- AIX
     * ```darwin```  -- MacOS X
     * ```linux```   -- Linux
     * ```smartos``` -- joyent SmartOS
     * ```solaris``` -- Sun Solaris
     * ```windows``` -- Windows

* ```BASHRC_OS_DISTRO``` -- The distro running (only set for Linux). Values for BASHRC_OS_DISTRO are:
     * ```debian``` (also on Ubuntu)
     * ```mandrake```
     * ```redhat```
     * ```suse```



Functions
----------

### Internal
* ```bashrc_determine_os``` defined in detect_os. Sets BASHRC_OS and BASHRC_OS_DISTRO.


