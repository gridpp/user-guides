#Putting Data on the Grid
We've now moved the
[local example workflow](../example-workflow-local/example-workflow-local.md)
to the
[Grid](../example-workflow-grid/example-workflow-grid.md).
However, we've still only used data that's been present
on our local system, and we've manually retrieved the output to our local
system.
To harness the full power of the Grid, we'll need to put data on it.
We'll use tools provided with DIRAC to do this, namely:
* The [DIRAC File Catalog Command Line Interface](dirac-dfc-cli.md) (DFC CLI);
* The [DIRAC command line tools](dirac-cl-tools.md);
* Some [first steps with the DFC's metadata functionality](dirac-metadata-first-steps.md).

First, though, let's look at some basic concepts in
grid-based data management.

##Storage Elements, File Catalogs, and Replicas
The first thing to wrap one's head around with distributed computing
is the notion that you don't really need to care about where your data
is stored.
You may well be used to this concept if you've dealt with
cloud-based storage services such as Dropbox, Google Drive,
or even Amazon S3 storage.
Your files are on one or more servers _somewhere_,
and all that you need to know are the file names and the directories
that they're in to access them later.

It’s the same with the grid. You upload your files to a grid
**Storage Element** (SE) and label them with a
**Logical File Name** (LFN) that gets registered in
something called a **File Catalog**.
If you make copies of a particular file - a **replica** - on one
or more additional SEs, the locations of these replicas are recorded
in the File Catalog too.

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
With most cloud-based storage services,
you won't even really care about the Storage Elements
(or their non-grid equivalents, whatever the they happen to be called)
and file replicas.
However, when considering running grid jobs at a particular grid site,
the location of your replicas can matter
(you'll want to make sure your data is available at sites that will run jobs
for your Virtual Organisation).
We’ll come back to all of these concepts - and provide concrete
examples - later.
</td>
</tr>
</table>

The GridPP DIRAC system provides a suite of tools to help you
manage all of this.
If you're familiar with UNIX-based file systems you should find it
all pretty straightforward.
We'll start with the
[DIRAC File Catalog Command Line Interface](dirac-dfc-cli.md).
