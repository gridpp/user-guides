#Your First Grid Job

OK, so you now know how to get your data on the grid
with the GridPP DIRAC service.
Now let's look at doing something with that data using the
grid.

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
The atomic unit of grid work is the
<strong>grid job</strong>.
Generally speaking,
a grid job takes your input data,
runs some software on that data on a grid Worker Node (WN),
and
gives you the output data back.
The input and output data can be on your local machine
or on a grid Storage Element (SE).
</td>
</tr>
</table>

To get you started,
we'll use the GridPP DIRAC service to submit a very, very simple
job to the grid using your GridPP DIRAC UI.
We won't interact with any grid-based data just yet,
but the following will take you through the basics of
job submission using the GridPP DIRAC service.

##A simple job
Following the example of the
[official DIRAC tutorials](https://github.com/DIRACGrid/DIRAC/wiki/JobManagement),
our simple job will list the contents of the Worker Node's working directory.
Create the following file in your text editor of choice:

```bash
$ cd ~
$ mkdir tmp-simple-job
$ cd tmp-simple-job
$ cat simple-job.jdl
JobName       = "Simple_Job";
Executable    = "/bin/ls";
Arguments     = "-ltr";
StdOutput     = "StdOut";
StdError      = "StdErr";
OutputSandbox = {"StdOut","StdErr"};
```

We'll look at what each bit of this file means shortly,
but first let's get our DIRAC environment ready:

```bash
$ cd ~
$ cd dirac_ui
$ . bashrc
$ dirac-proxy-init -g gridpp_user -M
[... DIRAC proxy generation output ...]
```

Returning to our (temporary) working directory,
we can submit the job with the following commands:

```bash
$ cd ~/tmp-simple-job
$ dirac-wms-job-submit simple-job.jdl
JobID = XXXXXX
```

where `XXXXXX` is the job ID assigned by the
DIRAC Workload Management System (WMS). 

And that's it!
You've submitted your first job to the grid.
While that works its way through the
WMS, let's take a moment to look at what each part of
`simple-job.jdl` means.

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
Job submission, and the running of the job itself,
is not an instant process.
Remember, we're talking about a nation-wide
distributed computing system that is handling
thousands of jobs (including yours) at any one time.
Patience, particularly with these first few jobs,
may be a necessary virtue!
</td>
</tr>
</table>

##Anatomy of a grid job

As we've submitted this simple grid job using the
DIRAC command line tool `dirac-wms-job-submit`,
we've used a text file written in the
_Job Description Language_ (JDL) to describe our job.
Each line of the JDL file tells the DIRAC WMS something
about what we want to run and how it should be run.
Looking at `simple-job.jdl`:

* `JobName`: This parameter gives the job a human-readble
name in the WMS. This is particularly useful in the
GridPP DIRAC job monitoring web interface (see below);
* `Executable`: The executable program file that the job
will run on the Worker Node. This can be a binary file
or executable script
uploaded with the job (see below),
a binary file or script distributed via CVMFS,
or any other (executable) file present on the Worker Node; 
* `Arguments`: The arguments to be supplied to the
executable named above;
* `StdOutput`: The filename for the terminal output.
This is useful for seeing what's happened as your job
has run on the Worker Node, and can be retrieved with your
job output by specifying the name in the
`OutputSandbox` parameter (see below);
* `StdError`: The filename for any error output.
Again, useful for debugging problems with your job;
* `OutputSandbox`: This tells the WMS which files to retrieve
from the Worker Node's working directory
when the job output is asked for.
Asking for `StdOut` and `StdErr` (or whatever you have named them)
is generally a useful thing to do - unless you expect them to
be huge...

So looking at `simple-job.jdl`,
we can see that the Worker Node will run:

```bash
$ ls -ltr
```

and we should be able to retrieve the output of this
(i.e. the working directory contents)
via the `StdOut` file which we'll get in the
`OutputSandbox`. (There shouldn't be any errors, so we
wouldn't expect a `StdErr` file to be written.)

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
Each line of a JDL file should end with a semi-colon.
Values for each parameter should be enclosed in
quotation marks, and if multiple parameters are supplied,
these should be enclosed in curly brackets.
</td>
</tr>
</table>

##Submitting a job

We've done this already, but the general command syntax is:

```bash
$ dirac-wms-job-submit <JDL file>
```

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
As with all DIRAC commands, you can use the
<code>--help</code> parameter to find all of the available
options.
</td>
</tr>
</table>

The command will tell you the job's ID number in the WMS.
It's useful to make a note of this, as you'll need it when...

##Finding out the job status
As noted above, running grid jobs is not an instant process.
It's therefore necessary to monitor the status of a given job
so that you know how it's filtering through the system
and (most importantly) when it's finished running.

You _can_ do this through the command line with the
following DIRAC command:

```bash
$ dirac-wms-job-status XXXXXX
```

where `XXXXXX` is the job ID number that you noted down above.

However, there is a nicer (and frankly, more information-rich)
way to monitor the status of your jobs.
Do you remember the GridPP DIRAC web portal from the
[First steps with GridPP DIRAC](../getting-on-the-grid/dirac-first-steps.md)?
Well, that provides a handy interface for monitoring your grid jobs:

* Go to https://dirac.gridpp.ac.uk and select
_Jobs_ &#x25BC; _Job Monitor_ from the top-left drop-down menu;
* Or, click on this direct link to the GridPP DIRAC
[Job Monitor](https://dirac.gridpp.ac.uk/DIRAC/GridPP/gridpp_user/jobs/JobMonitor/display).

You should then be able to see a list of your submitted jobs and
their respective statuses.

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
You can refresh the list using the <em>Refresh</em> button at the bottom of
the browser window.
</td>
</tr>
</table>

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
You can find out more about your job by right-clicking on
different cells in the job status table. Take some time to explore!
</td>
</tr>
</table>

All being well, the job should finish running:

* Its box in the job status table will go green;
* Its `Status` will display as "Done";
* `dirac-wms-job-status` will also return "Done" (as well as some other info). 

You'll then be able to go about...

##Retrieving the job output

```bash
$ dirac-wms-job-get-output XXXXXX
Job output sandbox retrieved in /home/gridpp/tmp-simple-job/XXXXXX/
```
where `XXXXXX` is the job ID. As promised, `StdOut` - the output
from the Worker Node as the job was run -
should have been retrieved and put in a folder with the same
name as the job ID:

```bash
$ cat XXXXXX/StdOut
total 4
-rw-r--r-- 1 plt00p00 plt00p00 657 Feb 18 13:10 job.info
```
(The owner, group, date and time information will of course
be different depending on where and when the job was run!)

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
<code>job.info</code> is a file containing information about the
job that is created in the Worker Node's working directory.
It is the only file that is present when <code>ls</code> runs
in this simple job.
</td>
</tr>
</table>

_Coming soon: uploading executable scripts and data with your grid jobs,
and retrieving input data from the grid!_
