#Creating a GridPP DIRAC UI
As well as its web portal,
DIRAC provides a command line-based User Interface (UI)
for interacting with the Grid.
New users are encouraged to use this for
job submission,
workload management,
and
data storage and management.
While the learning curve may be a little steeper
with a command line-based tool,
later you'll be able to use it in combination with
Ganga and the DIRAC Python API to handle the complex
processing and data management use cases
typically associated with large-scale scientific computing.

We'll create a GridPP DIRAC UI now.

##Prerequisites

Before proceeding, check you that you have:

* Command line access to an SL6 machine;
* Your converted Grid certificate files in the `~/.globus` directory;
* Successfully registered with a GridPP DIRAC-supported VO.

If you've followed all of the instructions in the UserGuide
so far (particularly if you're using a GridPP CernVM),
you should have all of this in place already.
If not, or you encounter any problems in the procedures below,
we would _strongly recommend_ working through the Checklist
and Testing parts of the previous sections
before submitting a
<a href='https://github.com/gridpp/user-guides/issues' target='_blank'>support request</a>.

##Installing the GridPP DIRAC UI
To create a GridPP DIRAC on your SL6 machine,
start a fresh terminal session on your SL6 machine
(we'll assume you're using a GridPP CernVM)
and enter the following commands:
```bash
[gridpp@localhost ~]$ cd ~
[gridpp@localhost ~]$ mkdir dirac_ui
[gridpp@localhost ~]$ cd dirac_ui
[gridpp@localhost dirac_ui]$ wget -np -O dirac-install http://lhcbproject.web.cern.ch/lhcbproject/dist/Dirac_project/dirac-install
[...output...]
[gridpp@localhost dirac_ui]$ chmod u+x dirac-install
[gridpp@localhost ~]$ ./dirac-install -r v6r13p9 -i 27 -g 2015-07-09
[...output...]
2015-10-05 12:08:14 UTC dirac-install [NOTICE] DIRAC properly installed
[gridpp@localhost dirac_ui]$ . bashrc 
[gridpp@localhost ]$ dirac-proxy-init -x # needs user cert password
Generating proxy... 
Enter Certificate password:
Proxy generated: 
subject      : /C=UK/O=eScience/OU=UniOfLondon/L=Computing/CN=ada lovelace/CN=proxy
issuer       : /C=UK/O=eScience/OU=UniOfLondon/L=Computing/CN=ada lovelace
identity     : /C=UK/O=eScience/OU=UniOfLondon/L=Computing/CN=ada lovelace
timeleft     : 23:59:59
path         : /tmp/x509up_u501
[gridpp@localhost ~]$ dirac-configure -F -S GridPP -C dips://dirac01.grid.hep.ph.ic.ac.uk:9135/Configuration/Server -I
[...output...]
```
That should configure your new GridPP DIRAC UI ready for use.
Close and re-open the terminal (or log out and in again)
before proceeding.

##Generating a DIRAC proxy
With your new GridPP DIRAC UI ready for use,
you should now be able generate a DIRAC-specific proxy
to be used as a member of a DIRAC-enabled VO.
If, for example, you were a member of the `gridpp` catch-all VO
you would use the following commands to generate a proxy as
a `gridpp_user`:
```bash
[gridpp@localhost ~]$ cd ~
[gridpp@localhost ~]$ cd dirac_ui
[gridpp@localhost dirac_ui]$ . bashrc
[gridpp@localhost dirac_ui]$ dirac-proxy-init -g gridpp_user -M
Generating proxy... 
Enter Certificate password:
Added VOMS attribute /gridpp 
Uploading proxy for gridpp_user... 
Proxy generated: 
subject      : /C=UK/O=eScience/OU=UniOfLondon/L=Computing/CN=ada lovelace/CN=proxy
issuer       : /C=UK/O=eScience/OU=UniOfLondon/L=Computing/CN=ada lovelace
identity     : /C=UK/O=eScience/OU=UniOfLondon/L=Computing/CN=ada lovelace
timeleft     : 23:53:59
DIRAC group  : gridpp_user
path         : /tmp/x509up_u501
username     : ada.lovelace
properties   : NormalUser
VOMS         : True
VOMS fqan    : ['/gridpp'] 

Proxies uploaded: 
 DN                                                          | Group       | Until (GMT) 
 /C=UK/O=eScience/OU=UniOfLondon/L=Computing/CN=ada lovelace | gridpp_user | 2016/03/24 14:40
```
If you get output that looks like the above, then it has all
worked.

> _You can check the status of your DIRAC proxy at any time
> with the_ `dirac-proxy-info` _command_.

Congratulations! You're all ready to start harnessing the
power of the Grid with the GridPP DIRAC UI.
Now we can start to submit jobs and manage data
using GridPP resources.
