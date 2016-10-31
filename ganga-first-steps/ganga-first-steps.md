# First steps: Hello World(s)!

It's something of a tradition to start any new computing activity
with an exercise that produces the phrase,
"[Hello, World!](https://en.wikipedia.org/wiki/%22Hello,_World!%22_program)"
with whatever you're doing. And it's not a tradition we'll be breaking
with now.
Distributed computing, however, is all about doing things on a bigger
scale - so we'll be saying "Hello" to many worlds all at the same time.
We'll do this using the
[Ganga](http://ganga.readthedocs.io) toolsuite.
By the end of this chapter you'll have used Ganga to submit multiple
jobs with a single command and check their output.
We won't use the grid yet - they will run on your local machine -
but thanks to Ganga and the other tools used by GridPP
making the switch to grid running is pretty straightforward.

Ready? Let's say "Hello!"

## Starting Ganga
[Ganga](http://ganga.readthedocs.io) is a Python-based toolkit
used for submitting jobs and managing data on the grid.
You can read more about it on its
[CERN page here](https://ganga.web.cern.ch/ganga/).
The code is all on
[GitHub](https://github.com/ganga-devs/ganga), of course.
Crucially, Ganga is available via CVMFS so
_you don't even have to install it_.
On your terminal with CVMFS access, Ganga can be started
by simply typing
```bash
$ source /cvmfs/ganga.cern.ch/runGanga.sh
```
After various welcome messages have been presented,
you should see the Ganga command prompt:
```bash
Ganga In [1]:
```

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
If you're familiar with
<a href='https://ipython.org/' target='_blank'>iPython</a>,
this prompt style should look very familiar!
</td>
</tr>
</table>

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
The number you see in the Ganga (iPython) prompt is the number of the
command that you've executed in the terminal. This is great for
interactive running, but rubbish for writing user guides.
We'll replace this is with an <code>X</code> in what follows.
</td>
</tr>
</table>

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
You will be using Ganga <em>a lot</em>. You may want to
create an <strong>alias</strong> for the Ganga start command in your
<code>~/.bashrc</code> file.
</td>
</tr>
</table>

All good so far? Great. Now you're ready to submit your first **job**.

## Submitting a Hello, World! job
Ganga has an iPython-esque command line interface for
real-time job management. Things like jobs are modelled using
Python objects. So creating and submitting a job is as simple
as this:

```bash
Ganga In [X]: j = Job()
Ganga In [X]: j.submit() 
```

You should see an output that looks like something like this:

```bash
INFO     submitting job X
INFO     job X status changed to "submitting"
INFO     Preparing Executable application.
INFO     Created shared directory: [temporary directory name]
INFO     Preparing subjobs
INFO     submitting job X to Local backend
INFO     job X status changed to "submitted"
```

What's going on here? Well, the `Job()` object has a bunch
of default settings that, on instantiation, create a
Hello, World! job that submits to the "Local" backend -
i.e. the machine you are running on.

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
The back-end is wherever you want your jobs to run -
your local machine, your local computing cluster,
or the grid (via GridPP DIRAC). The beauty of Ganga
is that you have the same interface for whichever you are
using - which makes switching between them a case of
tweaking some configuration files.
</td>
</tr>
</table>

In the time it has taken to read the above, you should see
the following output (press return if not).

```bash
INFO     job X status changed to "running"
INFO     Job X Running PostProcessor hook
INFO     job X status changed to "completed"
INFO     removing: [temporary directory name]
```

Your job has finished. You can check this - and the status
of any other jobs - using the `jobs` command, which produces
a neat little summary table of all of your jobs:

```bash
Ganga In [X]: jobs
Ganga Out [X]: 
Registry Slice: jobs (1 object)
--------------
    fqid |    status |      name | subjobs |    application |        backend |                             backend.actualCE |                       comment 
-------------------------------------------------------------------------------------------------------------------------------------------------------------
       X | completed |           |         |     Executable |      Localhost |                                  [host name] |
```

OK, so your job has run and finished, but where is the
famous phrase that signifies success? Well, Ganga manages your
job output for you in a series of output directories.
More on this later, but you can peek at the output with
the following command from Ganga:

```bash
Ganga In [X]: j.peek('stdout', 'more')
Hello World

```

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
We've used the <code>more</code> program to read the output,
but you can specify your own if you like...
</td>
</tr>
</table>

Ta da! You've submitted, run, completed, and checked the output
from, your first grid-like job. OK, so it didn't run on the
grid this time, but thanks to Ganga the process isn't actually
that different.

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
In fact the ability to run grid-like jobs locally is very
useful for testing your workflow out before unleashing it
on the grid...
</td>
</tr>
</table>

Finally, to tidy up:

```bash
Ganga In [X]: j.remove()
INFO     removing job X

```

You can check with the `jobs` command that the job has gone from the list.

Congratulations - you've submitted your first job! But we can do better than
that: with distributed computing, the idea is to break your problem into
bits and tackle them with multiple jobs: _divide and conquer_.
Let's see how easy this is to do with Ganga.
