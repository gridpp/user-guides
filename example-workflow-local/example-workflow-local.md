# An example workflow: local running
Hello, World! jobs are all very well, but we're guessing your
workflows are more complicated than a printing out a simple,
if polite, greeting.
We're now going to demonstrate the capabilities of
Ganga and the **CernVM-File System** (CernVM-FS, or CVMFS)
for running jobs with input data, remotely-managed software,
and output data.

### An aside: what is the CernVM-FS?
The [CernVM File System](http://cernvm.cern.ch/portal/startcvmfs)
is _"a network file system based on HTTP and optimized to deliver
software in a fast, scalable, and reliable way_".
It was developed to solve the problem of installing and
maintaining the software used by all of the different
particle physics communities involved with work at
[CERN](https://cern.ch).
Simply put, systems with the CernVM-FS installed have
instant access to a given community's software repositories
via the command line. This means it can be used:

* by community members working on university computing clusters
outside of CERN;
* by Worker Nodes (WN) anywhere on the grid where the repository is supported;
* by CernVM Virtual Machines.

You've already used CVMFS to run Ganga itself. But it can be used
to host your own software that will run anywhere on the Grid
(or, indeed, anywhere with access to CVMFS).

The example workflow we'll use comes from the
[CERN@school research programme](http://researchinschools.org/CERN/).
We'll take some raw particle detector data in ASCII format,
turn it into some pretty images of detected particles
using the Python `matplotlib` software,
and retrieve the frame information and images as output.

## The workflow itself
The workflow here is pretty straightforward:
* **Input**: raw detector data from a
[Timepix hybrid silicon pixel detector](http://medipix.web.cern.ch).
These ASCII text files represent the data (and detector settings)
recorded by a Timepix detector during a background measurement reading.
The dataset we use here is hosted on the web at
[FigShare](http://figshare.com). We will download a `zip` file
containing the data and upload it with our job.
* **Processing**: the data is processed with a Python script
in the CERN@school CVMFS repository called
`process-frames.py`.
This script in turn uses Python modules (both custom and
standard) that are also hosted on and sourced from CVMFS.
* **Output**: `process-frames.py` produces a log file,
a JSON containing information about the processed
data frames, and a directory of images representing the
particles detected in each frame.

We will create a workflow in Ganga that uploads the
input data we've downloaded from FigShare,
process it on our local machine,
compress the images into a single `tar` archive,
and retrieve the log file, JSON file, and `tar` archive
as output.

## Getting the input data
In your working directory, which we will associate with the
environment variable `$WORKINGDIR`, download the dataset as follows:
```bash
$ export WORKINGDIR=$PWD
$ cd $WORKINGDIR
$ wget http://files.figshare.com/2600426/CERNatschool_backgroundrad_dataset.zip
$ unzip CERNatschool_backgroundrad_dataset.zip
$ rm CERNatschool_backgroundrad_dataset.zip
$ ls
B06-W0212  E09-W0092  README.md
```

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
We could actually get our grid job to do this as part of the job.
Or we could tell our job to use input data that is already hosted
on a grid storage element. For simplicity, though, we will upload the
data we have just downloaded to our working directory with our job.
</td>
</tr>
</table>

We'll see how this is uploaded with the job below.

## Writing the executable
With our _Hello, World!_ job(s), we used the built-in
executable `echo` to print a simple string.
This workflow will use the shell script below, `run.sh`,
that contains the commands we want our job to execute.

```
$ vim run.sh
$ chmod a+x run.sh
$ cat run.sh
#!/bin/bash
#
# Add the Python packages from the CERN@school CVMFS
# repository to the PYTHONPATH environment variable.
export PYTHONPATH=/cvmfs/cernatschool.egi.eu/lib/python2.6/site-packages/:/cvmfs/cernatschool.egi.eu/lib64/python2.6/site-packages/:$PYTHONPATH
#
# Add CERN@school libraries to the LD_LIBRARY_PATH.
export LD_LIBRARY_PATH=/cvmfs/cernatschool.egi.eu/lib/:/cvmfs/cernatschool.egi.eu/lib64/:$LD_LIBRARY_PATH
#
# Add CERN@school libraries to the PATH.
export PATH=/cvmfs/cernatschool.egi.eu/lib64/:/cvmfs/cernatschool.egi.eu/lib/:$PATH
#
# Unzip the uploaded input data.
unzip CERNatschool_backgroundrad_dataset.zip
#
# Run the CVMFS-hosted Python script on the data.
python /cvmfs/cernatschool.egi.eu/code/particle-rate-plotter/process-frames.py $1 ./.
#
# Compress the images ready for retrieval.
tar -cvf output_images.tar PNG/
```

You should make `run.sh` in your `$WORKINGDIR` by copying and
pasting the above into your favourite text editor.

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
Don't forget to make the script executable with the <code>chmod</code>
command.
</td>
</tr>
</table>

## Creating, configuring, and submitting the job
We'll use Ganga's `execfile` functionality to create, configure,
and submit our job with a short Python script called
`local_job.py`, listed with explanatory comments below:

```
$ vim local_job.py # Copy and paste away!
$ cat local_job.py
## The Ganga job.
j = Job()

# Name the job.
j.name = "CERN@school_local_01"

# Tell Ganga it's running an executable: run.sh
j.application = Executable()
j.application.exe = File('run.sh')

# run.sh takes one argument - the dataset directory.
j.application.args = ['B06-W0212/2014-04-02-150255/']

# Specifiy which local files to upload with the job.
j.inputfiles = [ LocalFile('CERNatschool_backgroundrad_dataset.zip') ]

# Specify which files should be downloaded as output from the job.
j.outputfiles = [ LocalFile('frames.json'), LocalFile('log_process-frames.log'), LocalFile('output_images.tar') ]
j.submit()
```

You can then run this within Ganga using the `execfile` command
as before:

```bash
Ganga In [X]: execfile('local_job.py')
[... job output messages ...]
```

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
Make sure you are running Ganga from <code>$WORKINGDIR</code>
so that it can find <code>local_job.py</code>.
</td>
</tr>
</table>

You can monitor the status of the job as before with the
`jobs` command. As the job is actually doing some work now,
you may be able to see the job assume the `running` status.


## Getting the job output
Once the job has finished, you can view the output of the
text files as before with the `peek` command:
```bash
Ganga In [X]: j=jobs(X)
Ganga In [X]: j.peek('log_process-frames.log')
INFO:root: * Creating directory '././PNG'...
INFO:root:
INFO:root:* Found 60 datafiles.

```
To view the images you've created, you'll need to find where
they have been downloaded to on your local machine.
If the job ID was "1", you can do this with:

```bash
Ganga In [X]: j = jobs(1)
Ganga In [X]: j.outputdir
Ganga Out [X]: '/home/alovelace/gangadir/workspace/alovelace/LocalXML/1/output/'
```

```bash
$ cd $WORKINGDIR
$ cp /home/alovelace/gangadir/workspace/alovelace/LocalXML/1/output/output_images.tar output_images.tar
$ tar -xvf output_images.tar
PNG/
PNG/E09-W0092_2014-04-02-143123.png
[...]
PNG/E09-W0092_2014-04-02-142120.png
```

You can view these images with
the following command, which will bring up the
Eye Of Gnome image viewer (assuming you have it installed
on your local machine).
Use the arrow keys to move through the frames of data.

```bash
$ eog PNG/ &
```

So there we have it - we've run a (rather simple) workflow
on our local machine using Ganga. But here's the thing:
to move this workflow (and, indeed, most workflows) 
to the grid, we only need to do three things:

1. Configure the job to use the GridPP DIRAC backend;
1. Put our input data on the grid and configure our job to use this;
1. Configure the job to write the output data to the grid.

2) and 3) take a bit more work, but are optional (it really depends on
your input and output data as to what actually _needs_ to go
on the grid. But once you're setup for grid running, 1) only takes
a single line in your job configuration script:

```bash
j.backend=Dirac()
```

Ganga does the rest. Does that sound good?
Let's get you
[set up on the grid then](../getting-on-the-grid/getting-on-the-grid.md).
