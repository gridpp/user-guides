#Creating a Grid UI with a GridPP CernVM - Testing

* **Downloading the CernVM image**: Your `Downloads` folder
(or whichever location you chose to download the CernVM image file)
contains the image file.
```bash
analytical-engine:~ alovelace$ cd ~/Downloads
analytical-engine:Downloads alovelace$ ls -l | grep cernvm
cernvm-3.5.1.iso
```

* **Creating the CernVM**: When you start up your CernVM
from your virtualisation software,
you are eventually presented with a login screen.

```bash
Welcome to CERN Virtual Machine, version 3.5.1.4
  based on Scientific Linux release 6.6 (Carbon)
  Kernel 3.18.20-18.cernvm.x86_64 on an x86_64

IP Address of this VM: [IP address]
In order to apply cernvm-online context, use #<PIN> as user name.

localhost login: _
```

* **Registering with the CernVM Service**:
You can login via
<a href='https://cernvm-online.cern.ch/user/login' target='_blank'>this page</a>.
When you access
<a href='https://cernvm-online.cern.ch/' target='_blank'>this page</a>
you are redirected to the
<a href='https://cernvm-online.cern.ch/dashboard/' target='_blank'>CernVM Dashboard</a>.

* **Pairing your CernVM with the GridPP CernVM context**:
After selecting the GridPP CernVM context in the
<a href='' target='_blank'>CernVM Marketplace</a>
and clicking on the _Pair_ button on the right-hand panel,
you are presented with a six-digit number.
After entering the PIN into your CernVM's login screen
(preceeded by the hash symbol),
your CernVM reboots to display a graphical CernVM login screen.
Meanwhile, the CernVM Pairing web page has updated
to display the message,
> **Setup instance - Completed**
>
> Your vm is now paired with CernVM Online!
Upon logging in to your new CernVM with the username
`gridpp` and the password `gridpp`, you are presented
with the CernVM desktop.

* **Accessing your local machine's hard disk from you CernVM**:
You can access (from the command line or otherwise) folders on
your local machine's hard disk on the GridPP CernVM.
So (for example)
if you're using VirtualBox with the _Shared Folders_ functionality,
after adding the folders you want access to via the VM's _Settings_
and rebooting the VM you'll do something like this:
```bash
[gridpp@localhost ~]$ sudo usermod -a -G vboxsf gridpp
[sudo] password for gridpp: # Enter 'gridpp' here.
```
before loggin out and logging in again.
You'll then be able to access the folders you specified.
```bash
[gridpp@localhost ~]$ cd /media/sf_CardStack001 # Shared Folder "CardStack001" 
[gridpp@localhost sf_CardStack001]$ ls
punch-card-01.dat dad-poem-001.txt my-poem-005.txt
```
