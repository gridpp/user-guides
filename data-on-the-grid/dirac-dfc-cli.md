#The DFC Command Line Interface
The DIRAC File Catalog (DFC)
Command Line Interface (CLI),
a.k.a. the **DFC CLI**, provides a way of interacting with
DIRAC's File Catalog via - you guessed it - the command line.
The DFC CLI lets you manually upload and download files
to Storage Elements (SEs),
browse the DFC associated with your Virtual Organisation (VO),
create and remove directories in the DFC,
and manage the replicas associated with each entry in the DFC.

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
The DFC CLI is great for small-scale tasks such as
creating and tweaking test data sets,
but ultimately we will want to use scripts to help coordinate
large-scale upload operations and managing metadata
(i.e. data about the data).
</td>
</tr>
</table>

##Getting started with the DFC CLI

###Accessing the DFC CLI
The DFC CLI is accessed via a DIRAC command,
so we'll need to source our DIRAC environment
and generate a DIRAC proxy.

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
As ever, we will assume you have installed your
DIRAC UI in <code>/home/gridpp/dirac_ui</code> on your GridPP CernVM.
If you have a different setup, please be prepared to adjust the
commands accordingly.
</td>
</tr>
</table>

```bash
$ cd /home/gridpp/dirac_ui
$ . bashrc
$ dirac-proxy-init -g gridpp_user -M
Generating proxy... 
Enter Certificate password: # Enter your grid certificate password...
.
. [Proxy information-based output.]
.
```

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
If you wish to use a different VO, replace
<code>gridpp</code> with the name of the VO
in the commands in this section.
</td>
</tr>
</table>

The DFC CLI is then started with the following DIRAC command:

```bash
$ dirac-dms-filecatalog-cli 
Starting FileCatalog client

File Catalog Client $Revision: 1.17 $Date: 
            
FC:/>
```

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
We'll come back to the DIRAC command line tools in the next section,
but the <code>dirac-dms-</code> at the start of the command
refers to the DIRAC Data Management System tools.
All DIRAC commands are grouped in this
way which, combined with tab completion, can be very handy for
finding the command you're looking for!
</td>
</tr>
</table>

The `FC:/>` at the command prompt tells you that you're in the DFC CLI.
You can now explore the DFC using commands that are very similar
to those used with a typical UNIX file system.
Let's do this now.

###Finding your user space in the DFC
Let's start by listing the root directories in the DFC, which
will give us a list of the Virtual Organisations supported by
GridPP DIRAC:

```bash
FC:/> ls
cernatschool.org
gridpp
vo.londongrid.ac.uk
vo.northgrid.ac.uk
vo.scotgrid.ac.uk
vo.southgrid.ac.uk
```

We're using GridPP DIRAC as a member of `gridpp` VO,
so let's move into that directory.

```bash
FC:/> cd gridpp/user
```

If one hasn't been created for you already, you can
create your own user space on the VO's File Catalog
like so:

```bash
FC:/gridpp/user> cd a
FC:/gridpp/user/a> mkdir ada.lovelace
FC:/gridpp/user/a> chmod 755 ada.lovelace
FC:/gridpp/user/a> ls -la
drwxr-xr-x 0 ada.lovelace gridpp_user 0 2015-12-16 10:24:54 ada.lovelace 
FC:/gridpp/user/a> exit
```

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
If you don't know your DIRAC username (which should be used
as your user directory),
exit the DFC CLI and
use the <code>dirac-proxy-info</code>
command.
</td>
</tr>
</table>

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
Using the <code>-la</code> option with the <code>ls</code>
command works just as it does with the normal command line,
allowing you to see file owners, groups (VOs), permissions, etc.
</td>
</tr>
</table>

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
Don't forget to change the <strong>file permissions</strong> on
your files so that other users can't modify them.
</td>
</tr>
</table>

You've now got your own space on the GridPP DFC.
Let's put some files in it.

###Uploading files
Firstly, we'll need a file to upload. Any file will do,
but to keep things simple let's create one in a temporary
directory:

```bash
$ cd ~
$ mkdir tmp; cd tmp
$ vim TEST.md # Or whichever editor you use...
$ cat TEST.md
#Hello Grid!
This is a test **MarkDown file**.
```

Next we'll need to know which **Storage Elements**
are available to us.

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
<strong>Storage Elements</strong> "<em>are physical sites where data are
stored and accessed, for example, physical file systems,
disk caches or hierarchical mass storage systems.
Storage Elements manage storage and enforce authorization policies
on who is allowed to create, delete and access physical files.
They enforce local as well as Virtual Organization policies for
the use of storage resources.
They guarantee that physical names for data objects are valid
and unique on the storage device(s), and they
provide data access.
A storage element is an interface for
grid jobs and grid users to access underlying storage
through the
Storage Resource Management protocol (SRM),
the Globus Grid FTP protocol,
and possibly other interfaces as well.</em>"
<br />
<br />
<em>Credit: <a href='https://twiki.grid.iu.edu/bin/view/Documentation/Release3/NavAdminStorage#Storage_Elements' target='_blank'>Open Science Grid (2012)</a></em>
</td>
</tr>
</table>

We can list the available SEs with the following DIRAC command:

```bash
$ dirac-dms-show-se-status 
SE                           ReadAccess WriteAccess RemoveAccess CheckAccess 
=============================================================================
UKI-LT2-QMUL2-disk           Active     Active      Unknown      Unknown     
UKI-LT2-QMUL3-disk           Active     Active      Unknown      Unknown 
UKI-NORTHGRID-LIV-HEP-disk   Active     Active      Unknown      Unknown
```

While we don't need to know the details of where and how our data
will be stored on an SE, we do need to know its name.
We'll use the `UKI-LT2-QMUL2-disk` SE for now.
We add the file to the DFC as follows using the `add` command,
which takes the following arguments:

```
add <LFN> <Local file name> <SE name>
```

where:

* `<LFN>` is the **Logical File Name** (LFN) of the file in the
DFC. This can either be relative to your current position in the
DFC (which can be found with the `pwd` command in the DFC CLI),
or made absolute by preceeding the name with a slash `/`;
* `<Local file name>` should be the name of the local file
you want to upload. Again,
this can be relative to wherever you were on your local
system when you started the DFC CLI, or the absolute path to the
file on your local system;
* `<SE name>` is the name of the SE as retrived from the
`dirac-dms-show-se-status` command.

Let's add our file to the grid now.

```bash
$ dirac-dms-filecatalog-cli
Starting FileCatalog client

File Catalog Client $Revision: 1.17 $Date: 
            
FC:/> cd /gridpp/user/a/ada.lovelace
FC:/gridpp/user/a/ada.lovelace> mkdir tmp
FC:/gridpp/user/a/ada.lovelace> cd tmp
FC:/gridpp/user/a/ada.lovelace> add TEST.md TEST.md UKI-LT2-QMUL2-disk

File /gridpp/user/a/ada.lovelace/tmp/TEST.md successfully uploaded to the UKI-LT2-QMUL2-disk SE
FC:/gridpp/user/a/ada.lovelace/tmp>ls -la
-rwxrwxr-x 1 ada.lovelace gridpp_user 47 2015-12-16 11:47:28 TEST.md
```

And there we go! Your first file has been uploaded to
a Storage Element on the grid. Have a biscuit. You've earned it.

###Replicating files
Part of the joy of using the grid is being able to distribute
computational tasks to different sites. However, if you want
to look at the same data with a different task at different sites
in an efficient manner,
ideally you'd need copies of that data at those sites.
This strategy also makes sense from a backup/redundancy perspective.
We can achieve this on the grid by using _replicas_.

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
A <strong>replica</strong> is a copy of a given file that is
located on a different
<strong>Storage Element</strong> (SE).
The file is identified by its
<strong>Logical File Name</strong> (LFN) in the
<strong>DIRAC File Catalog</strong> (DFC).
Associated with each LFN entry is a list of SEs where
replicas of the file can be found.
</td>
</tr>
</table>

To list the locations of replicas for a given file catalog entry,
we use the `replicas` command in the DFC CLI:

```
replicas <LFN>
```

so continuing with our example:

```bash
FC:/gridpp/user/a/ada.lovelace/tmp>replicas TEST.md
lfn: /gridpp/user/a/ada.lovelace/tmp/TEST.md
UKI-LT2-QMUL2-disk srm://se03.esc.qmul.ac.uk:8444/srm/managerv2?SFN=//gridpp/user/a/ada.lovelace/tmp/TEST.md
```

We replicate files with the `replicate` command:

```
replicate <LFN> <SE name>
```

Let's replicate our test file to the Liverpool disk
and check that the replica list has been updated:

```bash
FC:/gridpp/user/a/ada.lovelace/tmp>replicate TEST.md UKI-NORTHGRID-LIV-HEP-disk
{'Failed': {},
 'Successful': {'/gridpp/user/a/ada.lovelace/tmp/TEST.md': {'register': 0.7740910053253174,
                                                            'replicate': 107.09606409072876}}}
File /gridpp/user/a/ada.lovelace/tmp/TEST.md successfully replicated to the UKI-NORTHGRID-LIV-HEP-disk SE
FC:/gridpp/user/a/ada.lovelace/tmp>replicas TEST.md
lfn: /gridpp/user/a/ada.lovelace/tmp/TEST.md
UKI-LT2-QMUL2-disk srm://se03.esc.qmul.ac.uk:8444/srm/managerv2?SFN=//gridpp/user/a/ada.lovelace/tmp/TEST.md
UKI-NORTHGRID-LIV-HEP-disk srm://hepgrid11.ph.liv.ac.uk:8446/srm/managerv2?SFN=//gridpp/user/a/ada.lovelace/tmp/TEST.md
```

Replicas can be removed with the `rmreplica` command:

```
rmreplica <LFN> <SE name>
```

Let's remove the Liverpool disk replica:

```bash
FC:/gridpp/user/a/ada.lovelace/tmp>rmreplica TEST.md UKI-NORTHGRID-LIV-HEP-disk
lfn: /gridpp/user/a/ada.lovelace/tmp/TEST.md
Replica at UKI-NORTHGRID-LIV-HEP-disk moved to Trash Bin
```

Finally, we can remove a file completely using the
(somewhat familiar) `rm` command:

```
rm <LFN>
```

Let's tidy up our test file:

```bash
FC:/gridpp/user/a/ada.lovelace/tmp>rm TEST.md
lfn: /gridpp/user/a/ada.lovelace/tmp/TEST.md
File /gridpp/user/a/ada.lovelace/tmp/TEST.md removed from the catalog
```

###Downloading files

Finally, we can download files using the DFC CLI with the
`get` command:

```
get <LFN> [<local directory>]
```

Note that the local directory argument is optional.
Let's download a test file from the `gridpp` examples
directory now:

```bash
FC:/> get /gridpp/userguide/WELCOME.md ./.
FC:/> exit
$ cat WELCOME.md
#Welcome to GridPP!

It looks like your download has worked. Congratulations!
$ rm WELCOME.md
```

As we said earlier, the DFC CLI is only useful for small-scale
operations. On our way to scaling up, we can look at
starting to automate our workflows using scripts.
In the next section we'll look at how the
[DIRAC command line tools](dirac-cl-tools.md)
can help with this.
