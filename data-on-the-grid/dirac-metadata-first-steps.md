#First steps with the DIRAC metadata functionality

##Finding files using metadata
When you're uploading vast amounts of data, it's nice to be able
to find it later.
**Metadata** - data _about the data_ - can help with this.
DIRAC allows you to assign metadata such as strings,
integers, and floating point numbers to files and directories
(via their Logical File Names in the DIRAC File Catalog).
You can then query the DFC to return a list of the files
you want.

For example, once you have sourced your DIRAC environment,
generated a proxy, and started the DFC CLI, you can
find all files associated with the `UserGuide` experiment
like so:

```bash
FC:/> find / experiment=UserGuide
Query: {'experiment': 'UserGuide'}
/gridpp/userguide/WELCOME.md
QueryTime 0.98 sec
```

We have assigned the value `UserGuide` to the file
`WELCOME.md` for the `experiment` element or index.
The `find` command in the DFC CLI performs the query for us.

```bash
FC:/> help find
 Find all files satisfying the given metadata information 
    
        usage: find [-q] [-D] <path> <meta_name>=<meta_value> [<meta_name>=<meta_value>]
    
FC:/> exit
```

In our query above, `<path>` was `/`
(i.e. search the entire catalog from the base directory),
`<meta_name>` was `experiment`
(i.e. a metadata string index indicating to which experiment
the data belongs),
and
`<meta_value>` was `UserGuide`
(OK, so the `UserGuide` isn't really an experiment - 
at least not in the scientific sense - but you get the idea!).

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
You can get a list of all of the available commands in the
DFC CLI by using the <code>help</code> command.
To list the instructions for a given command (as above),
type <code>help [command]</code>.
</td>
</tr>
</table>

There is only one file belonging to the `UserGuide` experiment
in the DFC, and it's a pretty harmless MarkDown file.
But you can hopefully see how, particularly when we start
using multiple metadata indices with different _types_,
DIRAC's metadata functionality is going to be pretty useful.

##Assigning metadata to a file
We can also use the DFC CLI to _assign_ metadata to our files.
Let's create a file with our favourite text editor
and upload it to the grid using the DFC CLI:
```bash
$ vim TODO.md
$ cat TODO.md
ToDo
====
* Email Charles re. engine
* Re-do punchcards
* Write to Dad
$ dirac-dms-filecatalog-cli 
Starting FileCatalog client

File Catalog Client $Revision: 1.17 $Date: 
            
FC:/> add /gridpp/user/a/ada.lovelace/TODO.md TODO.md UKI-LT2-QMUL2-disk
File /gridpp/user/a/ada.lovelace/TODO.md successfully uploaded to the UKI-LT2-QMUL2-disk SE
```
We can now set the `owner` index for the LFN using the
`meta set` command: 
```bash
FC:/> meta set /gridpp/user/a/ada.lovelace/TODO.md owner ada.lovelace
/gridpp/user/a/ada.lovelace/TODO.md owner ada.lovelace
```

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
Again, use <code>help meta</code> to see the syntax for the
<code>meta</code> commands.
</td>
</tr>
</table>

We can now find the file again using the `find` command:
```bash
FC:/> find / owner=ada.lovelace
Query: {'owner': 'ada.lovelace'}
/gridpp/user/a/ada.lovelace/TODO.md
QueryTime 0.01 sec
```
As we've said before, the DFC CLI is useful for
small-scale operations on your data.
Hopefully, though, you can start to appreciate the power of
**metadata** when it comes to organising your data
and performing analyses on it.

_Coming soon: managing your data with the DIRAC Python API!_
