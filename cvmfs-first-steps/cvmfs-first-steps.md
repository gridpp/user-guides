#A Taste of the Grid: the CernVM-FS

##Introduction: what is the CernVM-FS?
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

This last point is particularly exciting. It means we can get
an instant taste of distributed computing by running a
**grid job** on your own CernVM. 


<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
If you are not using a CernVM,
to proceed you will need to check if
your User Interface (UI) supports the CernVM-FS.
If it doesn't, you will need
to ask your systems administrator if it can be installed
or consider using a GridPP CernVM instead.
</td>
</tr>
</table>

##An example: the CERN@school CVMFS repository
For this demonstration we will use the CVMFS repository
belonging to the
[CERN@school Collaboration](http://cernatschool.web.cern.ch).
CERN@school is a programme that brings CERN into the classroom,
offering school students and teachers access to the CERN
technology and computing resources they need to perform their
own scientific research.

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
We will use the terms "CernVM-FS" and "CVMFS" interchangably throughout
the <em>UserGuide</em>. They mean the same thing.
</td>
</tr>
</table>

The CERN@school CVMFS repository contains code used to perform
physics analyses with
[Timepix](http://medipix.web.cern.ch) data.
To demonstrate the power of the CernVM-FS,
we will now run some of this code on your CernVM.

###Finding the code
The CVMFS repositories can be found in `/cvmfs/`
So to see what's in the CERN@school repository,
we can use the following command:

```bash
$ ls /cvmfs/cernatschool.egi.eu
code  lib  lib64  old  root
```

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
Until the repository has been used or asked for,
things like tab completion won't work on CVMFS
repositories. Using the <code>ls</code> command like this
is one way of loading it up.
</td>
</tr>
</table>

The code we want is, surprisingly enough,
in the `code` directory.

###Running the code
We'll run some Python code that processes data from
a Timepix detector. What the code does is irrelevant for
now; what we want to see is how software deployed via the
CernVM-FS is run on a WN - and, as it turns out, it's
run in the same way as any other software is run via the
command line. Try this:

```bash
$ python /cvmfs/cernatschool.egi.eu/code/particle-rate-plotter/process-frames.py
```

Has the software magically run? Well, no. Not quite.
Upon running that command, you should actually
see the following error:

```bash
$ python /cvmfs/cernatschool.egi.eu/code/particle-rate-plotter/process-frames.py
Traceback (most recent call last):
  File "/cvmfs/cernatschool.egi.eu/code/particle-rate-plotter/process-frames.py", line 36, in <module>
    from visualisation.visualisation import makeFrameImage
  File "/cvmfs/cernatschool.egi.eu/code/particle-rate-plotter/visualisation/visualisation.py", line 12, in <module>
    import pylab as plt
ImportError: No module named pylab
```

Oh noes! We don't appear to have the
[pylab](http://scipy.github.io/old-wiki/pages/PyLab)
module installed on our CernVM.
Normally when this happens, we'd just install the
required Python module onto our system
(assuming we had admin rights, of course).
However, we wouldn't want to do this on the
Worker Nodes we were using on the grid - life would
get messy very quickly.

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
In fact, that <em>was</em> the way things used to work before CVMFS.
Those were the days!
</td>
</tr>
</table>

So what do we do? Well, you may have noticed the
`lib` and `lib64` directories in the repository when we used
the `ls` command. These contain the software libraries we
need to run the CERN@school Python code, including the
`pylab` module.

All we need to do, therefore, is tell our system
(i.e. our CernVM) where to look for them in the
CVMFS repository. We do this by setting the
`PYTHONPATH` environment variable like so:

```bash
$ export PYTHONPATH=/cvmfs/cernatschool.egi.eu/lib/python2.6/site-packages/:/cvmfs/cernatschool.egi.eu/lib64/python2.6/site-packages/:$PYTHONPATH
```

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
If you don't know what an environment variable is,
we strongly recommend reading up on their usage.
See, for example, Hartl's
<em><a href='http://www.learnenough.com/command-line-tutorial' target='_blank'>Learn Enough Command Line to be Dangerous</a></em>.
</td>
</tr>
</table>

We can now try running the code again:

```bash
$ python /cvmfs/cernatschool.egi.eu/code/particle-rate-plotter/process-frames.py
*======================================*
* CERN@school - local frame processing *
*======================================*
usage: process-frames.py [-h] [-v] inputPath outputPath
process-frames.py: error: too few arguments
```

It works! All of the modules we need are provided via
the CERN@school CVMFS repository. All we need now is some
data upon which to run.

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
Later we will upload and retrieve data from the grid itself.
CVMFS should <em>not</em> be used for storing data.
</td>
</tr>
</table>

We'll use a dataset that features in one of the
CERN@school students' publications,
_[CERN@school: demonstrating physics with the Timepix detector](http://dx.doi.org/10.1080/00107514.2015.1045193)_.
This is stored on [FigShare](http://figshare.com),
which means it has its own
Digital Object Identifier (DOI) and can be cited as follows:

> T. Whyntie, _CERN@school: Background Radiation Measurements sample data set_, figshare
> [DOI: 10.6084/m9.figshare.1618851](http://dx.doi.org/10.6084/m9.figshare.1618851) (2015)

Use the following the commands to download the dataset to your
computer. Note the use of the `$DATA_DIR` environment variable
to save us a lot of typing later on.

```bash
$ cd ~
$ mkdir data; cd data
$ mkdir testdat; cd testdata
$ export DATA_DIR=$(pwd) # Set an environment variable for our data directory.
$ echo $DATA_DIR
/home/gridpp/data/testdata
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
For jobs running on the grid,
the data would either be uploaded to the Worker Node when the
job is sent to grid or retrieved from a specified
<strong>Storage Element</strong>.
We will come back to how data is managed on the grid later.
</td>
</tr>
</table>

Now that we have our code and our data in place,
we can run our (virtual) grid job:

```bash
$ export CODE_DIR=/cvmfs/cernatschool.egi.eu/code/particle-rate-plotter/
$ python $CODE_DIR/process-frames.py $DATA_DIR/B06-W0212/2014-04-02-150255/ $DATA_DIR/B06-W0212/2014-04-02-150255/
*
*======================================*
* CERN@school - local frame processing *
*======================================*
*
* Input path          : '/home/gridpp/data/testdata/B06-W0212/2014-04-02-150255/'
* Output path         : '/home/gridpp/data/testdata/B06-W0212/2014-04-02-150255/'
*
```

This particular Python script,
as the name may suggest,
processes raw frames of ASCII data from the
[CERN@school](https://cernatschool.web.cern.ch)
Timepix detectors into PNG images.
You can view these images with
the following command, which will bring up the
Eye Of Gnome image viewer.
Use the arrow keys to move through the frames of data.

```bash
$ eog B06-W0212/2014-04-02-150255/PNG/ &
```

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
If you want to find out more about what these data actually mean,
visit the <a href='https://cernatschool.web.cern.ch' target='_blank'>CERN@school website</a>.
</td>
</tr>
</table>

Let's take a moment to think about what we've just done.
In our virtual grid job, We have run a Python script that:

* was deployed by an external experimental collaboration
(CERN@school) via CVMFS; 
* depends on several non-standard Python modules;
* takes an input set of data (`RAW` ASCII text files)
and produces an output set of data (`PNG` image files),

all without installing any software or applying any sort of
additional configuration to our local machine.

Pretty sweet, no?

Now imagine doing that with thousands of machines across
the UK (or even the world) with _your software_ and
_your data_. Yeah. Exactly. Welcome to the grid.

Let's review what we've done with the [checklist](checklist.html).
