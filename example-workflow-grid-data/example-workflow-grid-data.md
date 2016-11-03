# Using Grid-based data in your workflow

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

## Putting data on the Grid

```bash
[DIRAC]
DiracLFNBase = /gridpp/user/a/ada.lovelace
```

```bash
j.outputfiles = [ DiracFile('output_images.tar') ]
```
