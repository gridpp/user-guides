#The DIRAC Command Line Tools

So you've mastered the DFC Command Line Interface.
Great stuff.
What you'll have probably noticed is that,
while it's great for small-scale operations,
it's not ideal for doing things with lots of files
on any sort of scale.
We will therefore want to take a look at the
**DIRAC command line tools** for data management.

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
All of the DIRAC command line tools start with
<code>dirac-</code>. The data management tools
start with <code>dirac-dms-</code>, as in
Data Management System.
Press the tab key after typing `dirac-dms-` to
see all of the available commands.
</td>
</tr>
</table>

Why are these commands useful? Well, it means you can
use _scripting_ to automate large-scale tasks
involving many files.
There are many ways to _script_ the DIRAC
(or indeed any command line)
commands.
You've probably got your own preferred method
that reflects your coding background.
For the purposes of the UserGuide,
we'll use simple bits of **Python** code
(along with Python-based file management libraries)
to generate some simple `bash` scripts that can then
be run to perform the DIRAC operations we want
to perform.

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
Of course, <code>bash</code> experts will be able to
write scripts that perform all of the operations below
purely in <code>bash</code>. This is left as an exercise for the
reader - answers on a punch card please!
(<em>Also, we'll be using Python for the DIRAC Python API,
so it's not a bad thing to use Python at this stage!</em>)
</td>
</tr>
</table>

##Uploading files
The DIRAC file upload command takes the following form:

```
$ dirac-dms-add-file <LFN> <FILE> <SE>
```
where:
* `<LFN>` is the Logical File Name (LFN) of the entry
for the file in the DIRAC File Catalog (DFC);
* `<FILE>` is the path to the file on your local machine, and;
* `<SE>` is the name of the destination Storage Element (SE).

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
Remember, you can find the names of the available SEs
with the <code>dirac-dms-show-se-status</code> command.
</td>
</tr>
</table>

Suppose we have a number of files on our local machine
in `/home/gridpp/mydata/`
that we want to upload to the grid.
The following Python code will generate a `bash` script
that will upload them to one of the Queen Mary Storage Elements:

```python
$ cat make_upload_script.py
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import os, glob

data_path = '/home/gridpp/mydata'

lfn_dir = '/gridpp/user/a/ada.lovelace/mydata/'

se = 'UKI-LT2-QMUL2-disk'

s = "#!/bin/bash\n"

for my_file in sorted(glob.glob(data_path + "/*")):
    base_name  = os.path.basename(my_file)
    upload_lfn = os.path.join(lfn_dir, base_name)
    s += "dirac-dms-add-file %s %s %s\n" % (upload_lfn, my_file, se)

with open("upload_script.sh", "w") as sf:
    sf.write(s)
```

After you've generated a proxy and sourced the DIRAC
environment, you can run the generated script as follows:

```bash
$ python make_upload_script.py
$ chmod a+x upload_script.sh
$ . upload_script.sh
```

The results of this will, of course, depend on the contents
of `/home/gridpp/mydata/`, but all being well you should see the
message:

```
Successfully uploaded file to UKI-LT2-QMUL2-disk
```

(or whichever SE you specified in your Python code)
after each file has been uploaded.

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
If you're uploading a lot of files,
you may wish to consider using something like the
<code>screen</code> tool so that you can log off your
terminal session and come back to it later.
</td>
</tr>
</table>

And there we go! Multiple file uploads,
all registered in the DIRAC File Catalog,
using a DIRAC command line tool and a bit of
(admitedly slightly clumsy) coding.

##Replicating files

Now, as we did with the DFC CLI, we can also
make replicas of files,
list information about the replicas of a given file,
and
remove replicas
with the following command line tools:

```
dirac-dms-replicate-lfn <LFN> <SE>
dirac-dms-lfn-replicas <LFN>
dirac-dms-remove-replicas <LFN> <SE>
```

Likewise, we can take the same approach with...

##Downloading and removing files

```
dirac-dms-get-file <LFN>
dirac-dms-remove-files <LFN>
```

i.e. the DIRAC command line tools exist for these operations.
However, getting information from the DFC about which
files you would like to replicate, download, remove, etc.
is non-trivial when taking the command line approach.
This is especially true if you're writing scripts.

One approach is to use the **metadata** functionality
the DIRAC File Catalog provides to find files of interest.

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
<strong>Metadata</strong> is <em>data about the data</em>.
By assigning metadata to the files we upload to the
DIRAC File Catalog, we can perform queries that will
select only the files we are interested in.
It also helps us to manage our data.
We'll find out more about the DFC's metadata functionality later.
</td>
</tr>
</table>

The `dirac-dms-find-lfns` command finds LFNs based on
the DFC path and metadata query supplied as options.
For example, to find all files in the DFC that
have been assigned to the experiment  `UserGuide`,
we can type:

```bash
dirac-dms-find-lfns Path=/ "experiment=UserGuide"
{'experiment': 'UserGuide'}
/gridpp/userguide/WELCOME.md
```

`experiment` here is the **metadata element** or **index**.
This is a string assigned to the file's LFN that,
in this case, has the value `UserGuide`.
We can use the results of this to download the files
we want.

```bash
$ dirac-dms-get-file /gridpp/userguide/WELCOME.md
{'Failed': {},
 'Successful': {'/gridpp/userguide/WELCOME.md': '/home/gridpp/tmp/WELCOME.md'}}
$ cat WELCOME.md
#Welcome to GridPP!

It looks like your download has worked. Congratulations!
```

Let's take a closer look at the DFC's 
[metadata functionality using the DFC CLI](dirac-metadata-first-steps.md).
