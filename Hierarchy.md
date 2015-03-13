# Introduction #

We want to specify our OS' filesystem hierarchy only because it will be a reminder for us and it will explain briefly the [Filesystem Hierarchy Standard (FHS)](http://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard) v2.3 (the current version since 2004) which is the one we use.


# The Filesystem Hierarchy Standard #

Since the early years comunities of researchers, IT enthusiasts and foundations involved in Unix-like OSes development were discussing about how the filesystem hierachy had to be implemented. For some time every team or single developer chose its own standard but this lead soon to incompatibilities. This happened since a group of people decided to standardize this structure. Briefly, now we are in full development of the 3.0 standard and we have a (old, unfortunately) standard called [The LHS v2.3](http://www.pathname.com/fhs/pub/fhs-2.3.html) which defines a common structure idea to use in our OSes development.

## Version 2.3 ##

A one-line shell command will create the entire structure, as following:
```sh

mkdir -p /{bin,boot,dev,etc/{opt,X11,sgml,xml},home,lib{/X11,/modules,32,64},media,mnt,opt,root,sbin,srv,tmp,usr/{bin,games,include/{,bsd},lib{/X11,32,64},local/{bin,etc,games,include,lib,man,sbin,share,src},sbin,share/{dict,doc,games,info,locale,man/{en,it}/man{1,2,3,4,5,6,7,8},misc,nls,sgml/{docbook,tei,html,mathml},xml/{docbook,html,mathml},zoneinfo},src,X11R6/{bin,lib,include}},var/{account,cache/{fonts,man,www},crash,games,lib,local,lock,log,mail,opt,run,spool/{lpd/printer,mqueue,news,rwho,uucp},tmp,yp}}
```

  * bin - Essential command binaries
  * boot - Static files of the boot loader
  * dev - Device files
  * etc - Host-specific system configuration
    * opt - Configuration for /opt
    * X11 - Configuration for the X Window system (optional)
    * sgml - Configuration for SGML (optional)
    * xml - Configuration for XML (optional)
  * lib - Essential shared libraries and kernel modules
    * modules - Loadable kernel modules (optional)
  * lib32 - Essential shared libraries and kernel modules (x86)
  * lib64 - Essential shared libraries and kernel modules (x86\_64)
  * media - Mount point for removeable media
  * mnt - Mount point for mounting a filesystem temporarily
  * opt - Add-on application software packages
    * `<package>` - Static package objects
  * proc - Linux kernel and process information virtual filesystem
  * root - Home directory for the root user (optional)
  * sbin - Essential system binaries
  * srv - Data for services provided by this system
  * tmp - Temporary files
  * usr - Secondary hierarchy
    * bin - Most user commands
    * games - Games and educational binaries (optional)
    * include - Header files included by C programs
      * bsd - BSD compatibility include files (optional)
    * lib - Libraries
      * X11 - If /lib/X11 exists, /usr/lib/X11 must be a symbolic link to /lib/X11, or to whatever /lib/X11 is a symbolic link to.
    * lib32 - Libraries (x86)
    * lib64 - Libraries (x86\_64)
    * local - Local hierarchy (empty after main installation)
      * bin - Local binaries
      * etc - Host-specific system configuration for local binaries; must be a link to /etc/local
      * games - Local game binaries
      * include - Local C header files
      * lib - Local libraries
      * man - Local online manuals
      * sbin - Local system binaries
      * share - Local architecture-independent hierarchy
      * src - Local source code
        * linux - Linux kernel source code (symlink to a kernel source code tree)
    * sbin - Non-vital system binaries
    * share - Architecture-independent data
      * dict - Word lists (optional)
      * doc - Miscellaneous documentation (optional)
      * games - Static data files for /usr/games (optional)
      * info - GNU Info system s primary directory (optional)
      * locale - Locale information (optional)
      * man - Online manuals
        * `<locale>` - l10n language code
          * man1 - User programs (optional)
          * man2 - System calls (optional)
          * man3 - Library calls (optional)
          * man4 - Special files (optional)
          * man5 - File formats (optional)
          * man6 - Games (optional)
          * man7 - Miscellaneous (optional)
          * man8 - System administration (optional)
      * misc - Miscellaneous architecture-independent data
      * nls - Message catalogs for Native language support (optional)
      * sgml - SGML data (optional)
        * docbook - docbook DTD (optional)
        * tei - tei DTD (optional)
        * html - html DTD (optional)
        * mathml - mathml DTD (optional)
      * xml - XML data (optional)
        * docbook - docbook XML DTD (optional)
        * xhtml - XHTML DTD (optional)
        * mathml - MathML DTD (optional)
      * zoneinfo - Timezone information and configuration (optional)
    * src - Source code (optional)
    * `X11R6` - XWindow System, version 11 release 6 (optional)
      * bin - Most plain XWindow application binaries
      * lib - Plain XWindow shared libraries
      * include - Header files included in plain XWindow applications
  * var - Variable data
    * account - Process accounting logs (optional)
    * cache - Application cache data
      * fonts - Locally-generated fonts (optional)
      * man - Locally-formatted manual pages (optional)
      * www - WWW proxy or cache data (optional)
      * `<package>` - Package specific cache data (optional)
    * crash - System crash dumps (optional)
    * games - Variable game data (optional)
    * lib - Variable state information
    * local - Variable data for /usr/local
    * lock - Lock files
    * log - Log files and directories
    * mail - User mailbox files (optional)
    * opt - Variable data for /opt
    * run - Data relevant to running processes
    * spool - Application spool data
      * lpd - Printer spool directory (optional)
        * printer - Spools for a specific printer (optional)
      * mqueue - Outgoing mail queue (optional)
      * news - News spool directory (optional)
      * rwho - Rwhod files (optional)
      * uucp - Spool directory for UUCP (optional)
    * tmp - Temporary files preserved between system reboots
    * yp - Network Information Service (NIS) database files (optional)