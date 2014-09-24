patched-bash-4.3
================

patched-bash-4.3 for CVE-2014-6271


This is just bash 4.3 , pulled from the gnu website, and patched with the patches available on 9/24/2014

Don't use this, if you don't know and trust me.  Build it yourself.

I'm putting this on github so I can point friends and co-workers here.

#### For hotpatching this in a SmartOS zone (like in JPC):

- clone this repo

``` git clone https://github.com/ryancnelson/patched-bash-4.3 ```

- ```cd bash-4.3```
- ```make clean ; ./configure ; make ; make install ```
- look at 
```
/usr/local/bin/bash --version 
GNU bash, version 4.3.25(1)-release (i386-pc-solaris2.11)
Copyright (C) 2013 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>

This is free software; you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

```

- mount this file, using the lofs mount trick , ON TOP of /usr/bin/bash :
  - you may need to reboot to kill off any currently running bash shells
  - after reboot, log back in, and run ``` exec /bin/sh ``` to confirm you're not using bash at the moment.
  - ``` ps -ef | grep bash ``` should return nothing.
  - then, mount /usr/local/bin/bash over /usr/bin/bash with: ```mount -F lofs /usr/local/bin/bash /usr/bin/bash ```
  - this lofs mount is not permenant.  re-do after reboots, or wait for a patched platform image.

- confirm that ```/usr/bin/bash --version ``` returns the new 4.3 version you expect after the ```lofs mount``` command
