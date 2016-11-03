# Using Grid-based data in your workflow
The example workflow we've used so far isn't particularly sophisticated,
but it does allow us to demonstrate the final key concept
we'll look at here: incorporating Grid-based data in your
workflows. Below we'll go through:

* Putting the initial input data onto the Grid;
* Using that data as the input to your workflow;
* Writing the output data from your workflow to the Grid;
* Retrieving the output from the Grid.

You'll need to have worked through
[this section](../example-workflow-grid/example-workflow-grid.md)
first - mainly because we actually only need to tweak a few lines
to achieve what we want!

## Putting our input data onto the Grid
The first thing to do is put the ZIP file containing the
raw frame data into your user area on the DFC.
You know how to do this
(if not, have another look at
[this section](../data-on-the-grid/data-on-the-grid.md))
so now we're getting into the realm of user areas, VOs, etc.
we're not going to give the explicit commands for this part.
We'll also leave you to come up with a LFN for the file,
and choose which SE to use (you might have a favourite by now).

* Download the ZIP file to your working directory;
* Upload it to your user area in your VO's area in the DFC;
* **Note down the LFN you assigned the file**. You'll need this below.

_OK, we'll give you a hint. An LFN the user `ada.lovelace`,
member of the `gridpp` VO, might use, might look something like this_:
```
LFN:/gridpp/user/a/ada.lovelace/userguide/example-workflow-grid-data/CERNatschool_backgroundrad_dataset.zip
```

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
While the directories don't strictly exist with LFNs,
it's useful to keep things organised with sensible structuring/naming
conventions. Use the DFC CLI to create directories in your user area
as required.
</td>
</tr>
</table>


## Getting data from the Grid
Thanks to Ganga, there's actually not much to using a Grid-hosted
data file as input. All you need to do is add a 
`DiracFile` to the job's `inputputfile` list with the
LFN as the input argument. So Ada's modified `dirac_job.py` script
would have the line:

```bash
j.inputfiles = [ DiracFile('LFN:/gridpp/user/a/ada.lovelace/userguide/example-workflow-grid-data/CERNatschool_backgroundrad_dataset.zip') ]
```

The job will now retrieve the ZIP file from whichever Storage Element
1) has a replica of the file and/or 2) is closest to the site running the
job to the working directory, just as it would with the `LocalFile`.

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
In fact, GridPP DIRAC will work out where is best to send your job based
upon where you have replicas of the file (i.e. which SEs you added/replicated
it on). So once you're into optimisation territory, <strong>replica management</strong>
is something to think about.
</td>
</tr>
</table>

## Writing data to the Grid
What about the output data? If you have an intermediary data layer
(i.e. output that is used as input for another job/workflow)
you may wish to write the output to the Grid.
This is possible with a few tweaks, but there's a slight subtlety:
GridPP DIRAC will assign LFNs for your job output based on
the DIRAC job ID and an LFN base specified in your `.gangarc` file.
This can be set with something like the following:

```bash
[DIRAC]
DiracLFNBase = /gridpp/user/a/ada.lovelace
```

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
Make sure you set this before starting Ganga and submitting your job(s).
</td>
</tr>
</table>

Specifying which files get written to the Grid is then pretty similar
to specifying the input files - switch the `LocalFile` to `DiracFile`:

```bash
j.outputfiles = [ DiracFile('output_images.tar') ]
```

With these changes made (and maybe a change of job name),
you can now submit your job.

## Retrieving the output from the Grid
You
[already know](../data-on-the-grid/data-on-the-grid.md)
how to retrieve files from the Grid.
The only extra detail you'll need to know is the DIRAC job ID.
**This is different to the job ID in Ganga**.
Both can be obtained with the following commands within
Ganga:

```bash
Ganga In [X]: j.id
Ganga Out [X]: 1

Ganga In [X]: j.backend.id
Ganga Out [X]: 1234567
```

(i.e. the DIRAC ID will have many more digits.)

The DIRAC ID will determine the LFN the output files are assigned.
So once the job has finished running, you should end up with something
like this:

```bash
$ dirac-dms-filecatalog-cli 
Starting FileCatalog client

File Catalog Client $Revision: 1.17 $Date: 
            
FC:/> cd gridpp/user/a/ada.lovelace/
FC:/gridpp/user/a/ada.lovelace>ls
1234
FC:/> ls 1234
1234567
FC:/> ls 1234/1234567
frames.json
output_images.tar
```

So the full LFN for the image archive is:

```bash
LFN:/gridpp/user/a/ada.lovelace/1234/1234567/output_images.tar
```

This can be used to retrieve the file in the ways we have
described already - or used as an `inputfile` to another job.

So there we go - we've completely Grid-ified our example workflow.
You should now have all of the tools you need to start making your own
workflows Grid-ready.
Of course, there's a lot more that can be done
and we'll mention some of the more advanced topics in the
[next section](../whats-next/whats-next.md).
But you should have plenty to get your teeth into for now!
