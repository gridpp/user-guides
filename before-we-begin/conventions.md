#Conventions in this guide
The conventions used in the _GridPP UserGuide_ are, by and large,
self-explanatory.
Here we'll look at a few that might not be.

##The command line
Following [Hartl](https://www.railstutorial.org),
we'll present command line examples using a Unix-style
command line prompt (a dollar sign), as follows:

```bash
$ echo "Hello, Grid!"
Hello, Grid!
```

i.e. you type what follows the dollar sign, and hopefully
see the same (dollar sign-less) output in your terminal.

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
Computer systems are always going to vary from machine to machine,
so you may not see exactly the same output from a given command.
We've tried to eliminate this as much as possible
by using the CernVM (see later) but more often than not
a combination of common sense and Googling the output should
confirm if you're on the right track.
</td>
</tr>
</table>

Where possible we'll use bash environment variables to
account for differences in working directories.
However, if a particularly user-specific input is needed
we'll use square brackets to denote parts of the command
that require input specific to your circumstances.
For example, when setting your working directory
environment variable `WORKING_DIR`, we'd write this:

```bash
$ export WORKING_DIR=[Your working directory.]
$ echo $WORKING_DIR
[The value of $WORKING_DIR, hopefully your working directory.]
```

which would actually be completed using:

```bash
$ export WORKING_DIR=/home/alovelace/grid-stuff/
$ echo $WORKING_DIR
/home/alovelace/grid-stuff/
```

##Code listings
Generally speaking, we have tried to avoid listing large
swathes of code in the _UserGuide_ itself - that's what
GitHub is for. From time-to-time it may be useful to
include a code snippet like the following:

```python
#!/usr/bin/env python
print("* This works!")
```

Following [Hartl](https://www.railstutorial.org),
we will use vertical dots to represent code omitted for the
sake of brevity:

```Python
#!/usr/bin/env python

class GridJob:
    .
    .
    .
    def submit(self, id):
        self.id = id
        .
        .
        .
```

These dots should not be copied into your code. Obvs.

##Hints, warnings, and information
The _GridPP UserGuide_, like many instructional handbooks,
uses little pop-out boxes to highlight important points
throughout the text.

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
This is a hint. Hint boxes are used for pointing out things
that might be useful while carrying out the task being described
(particularly where we have received user feedback on a given step!).
</td>
</tr>
</table>

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
This is a warning.
These are used to flag up potential pitfalls or issues
you may need to be aware of to avoid making mistakes
or doing Something Bad.
</td>
</tr>
</table>

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
This is a point of information.
These boxes will generally present things that
may not directly relate to the topic being discussed
but are nonetheless interesting.
</td>
</tr>
</table>

Thanks to Font Awesome for the icons! They're, um, awesome.

##Checklists
Once you've waded through the waffle associated
with a given section,
you'll be presented with a **checklist** section
that will give you a simple, bullet-pointed list
of the things you should be able to do once
you've read that section.
You should go through these to make sure you
have done them and, more importantly,
understood them.
If not, re-read the section.
Alternatively, you could plough on and
try the tests - see below - to see if it makes
more sense when you try to actually do something
based on what you've just read.

##Testing
All well-written, well-packaged code should come
complete with **unit tests**; scripts or bits of code
that can be run to test whether one's software is
working as expected (especially during development
as changes are made and new versions are produced).
We can try to emulate this approach
by trying to test the success of each of
the steps taken while following the instructions
presented in the _UserGuide_.
At the end of each section you will therefore find a
**Testing** page that will present a number of tasks
or tests for you to complete to verify that you have followed
the _UserGuide_.
As a rule you should not proceed to the next section
until you have passed all of these tests.

If you're struggling,
there are plenty of ways to get help and support.
We'll find out more about these in the
[next section](getting-help.html).
