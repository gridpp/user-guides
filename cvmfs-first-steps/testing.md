#A Taste of the Grid: the CernVM-FS - Testing

* **Looking at the contents of a CVMFS repository**:
The following command produces the following output.
```bash
$ ls /cvmfs/cernatschool.egi.eu/
code  lib  lib64  old  root
```

* **Setting up your environment**:
The following command produces the following output.
```bash
$ echo $PYTHONPATH
/cvmfs/cernatschool.egi.eu/lib/python2.6/site-packages/:/cvmfs/cernatschool.egi.eu/lib64/python2.6/site-packages/:
```

* **Running code from the CERN@school CVMFS repository**:
You have followed the instructions
[here](cvmfs-first-steps)
and ended up with a directory full of
[Timepix](https://medipix.web.cern.ch)
frame images. You can view these images with a
locally-installed image viewer (e.g. `eog`).
