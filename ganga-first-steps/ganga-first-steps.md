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
