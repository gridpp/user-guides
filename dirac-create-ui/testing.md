#Creating a GridPP DIRAC UI - Testing

* **Installing the GridPP DIRAC UI**:
The following commands produce the following output:
```bash
[gridpp@localhost ~]$ cd ~/dirac_ui
[gridpp@localhost ~]$ ls
DIRAC                    cshrc               etc
Linux_x86_64_glibc-2.12  defaults-DIRAC.cfg  scripts
bashrc                   dirac-install       version-2015-07-09.txt
```

* **Sourcing the DIRAC environment**:
You can test the DIRAC environment variables have been
set using the `echo` command.
For example, on a GridPP DIRAC UI setup on a CernVM
using the instructions here, you would get:
```bash
[gridpp@localhost ~]$ echo $DIRAC
/home/gridpp/dirac_ui
```
If the DIRAC home directory is not listed, the environment
variables have not been set correctly.

* **Generating a DIRAC proxy**:
You can test if your proxy generation has been successful by
using the `dirac-proxy-info` command.
