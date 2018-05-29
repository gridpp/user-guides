#What's Next?

## Uploading your software to CVMFS
To start with, and if your software package/packages is/are small enough,
you can probably get away with uploading your software as `LocalFile`s
with your Grid job (perhaps using an archive file).

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
In fact, you may prefer this approach as http-based CVMFS repositories are
world-readable.
</td>
</tr>
</table>

However, at some point you and/or your Virtual Organisation
are going to want your own CVMFS repository.
For small, UK-based VOs the best way to do this is on the
[RAL Tier-1 Stratum-0](https://www.gridpp.ac.uk/wiki/RAL_Tier1_CVMFS).
[Contact us](mailto:info@gridpp.ac.uk) to find out more about doing this -
access to the repository is governed by your Grid certificate.

In short, the process of uploading your software amounts to:
* **Generating a proxy with DIRAC**: as this will be used to
determine who you are and which repository you are accessing;
* **Logging in to the repository**:
You can then log in to your CVMFS repository with:

```bash
$ gsissh -p 1975 cvmfs-upload01.gridpp.rl.ac.uk
Last login: [Date/time] from [hostname]

   _. _.   o| _ ._
  (_|(_||_|||(_)| |
       |

          Location: r89.harwell.europe hpd r89rack137
            Branch: cc34/cvmfs-uploader (sandbox)
         Archetype: ral-tier1
       Personality: cvmfs-uploader
  Operating System: sl640-x86_64
     Snapshot Date: 2016-10-26

[{vo-name}sgm@cvmfsXXXXX ~]$ cd cvmfs_repo
bin lib code README.md
```

* **Retrieve your software**:
You can now place your software in the repository, arranging it
however works best for you. If your code is hosted in an online
Git-based repository, simply `git clone` it straight to an
appropriate directory.

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
You can take inspiration from other VOs. For example, you can browse
the ATLAS experiment's (CERN-hosted) CVFMS repository with:
<code>$ ls /cvmfs/atlas.cern.ch/</code> and so on.
</td>
</tr>
</table>


<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
All files and directories part of a CVMFS repository must be kept 'read'-able by everyone e.g.
<br>
<code>  find ./ -type d -exec chmod go+rx {} \; </code><br>
<code>  find ./ -type f -exec chmod go+r {} \; </code><br>

The bundle will not publish if it contains any non-readable files.

</td>
</tr>
</table>

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
Once put into the repository, it can be several hours before it
becomes available on the worker nodes - it's not instant.
Make sure your software is well-tested before putting it up - 
CVMFS is not appropriate for software under development!
</td>
</tr>
</table>

However, once it _is_ on there, it's available everywhere.
Which is nice.

## Advanced DIRAC functionality
DIRAC has a great deal of functionality of its own,
particularly when you start looking at the Python API.
However, Ganga provides a nice wrapper for much of this
so you shouldn't need to touch it.
You can find out more on the
[DIRAC homepage](http://diracgrid.org/), and check out the
source code on their
[GitHub page](https://github.com/DIRACGrid).

## Advanced Ganga functionality
Likewise, there is a lot more to Ganga than we have covered here.
Ganga has its own documentation page: http://ganga.readthedocs.io
which features things like:
* Configuration;
* Job manipulation;
* Splitters;
* Post-processors;
* Queues;
* Etc.

The [GitHub repository](https://github.com/ganga-devs/ganga)
is also worth watching for the latest updates and developments,
as well as raising any bugs or problems you may have in the
[Issues](https://github.com/ganga-devs/ganga/issues) section.

## And finally...

Moving your workflow to the Grid won't necessarily be straightforward,
but at GridPP we're [here to help](../before-we-begin/getting-help.html) -
if you've got a problem, just ask!
To keep up to date with the UserGuide,
watch the
[_UserGuide_ GitHub repository](https://github.com/gridpp/user-guides)
to be notified of
[Issues](https://github.com/gridpp/user-guides/issues)
and Pull Requests relating to additions or improvements
to the _UserGuide_.

Many thanks for reading so far, and happy Gridding!

_Return to the [GridPP homepage](https://www.gridpp.ac.uk)_.
