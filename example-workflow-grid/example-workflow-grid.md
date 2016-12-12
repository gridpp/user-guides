# Moving the example workflow to the grid
Now that you have your Grid certificate, and it is installed
in your browser and in your `~/.globus` directory,
you're ready to try submitting a job to the Grid with DIRAC.

## Activate DIRAC!
Thanks to CVMFS and the
[Ganga team](https://github.com/ganga-devs/),
activating the GridPP DIRAC functionality is easy:

```bash
$ source /cvmfs/ganga.cern.ch/dirac_ui/bashrc
```

You should now be able to tab-complete `dirac-` to see all of the
DIRAC commands that are available.

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
The inclusion of the pre-configured DIRAC UI in the Ganga
CVMFS repository means that you no longer need to install
your own DIRAC UI. Which makes life <em>a lot</em> easier...
</td>
</tr>
</table>

## Generate a Grid proxy
With DIRAC activated via CVMFS,
you should now be able generate a DIRAC-specific proxy
to be used as a member of a DIRAC-enabled VO.
Your proxy is a file that identifies you on the Grid,
letting the system know that you're good for using its resources.
If, for example, you were a member of the `gridpp` catch-all VO
you would use the following commands to generate a proxy as
a `gridpp_user`:

```bash
$ dirac-proxy-init -g gridpp_user -M
Generating proxy... 
Enter Certificate password:
Added VOMS attribute /gridpp 
Uploading proxy for gridpp_user... 
Proxy generated: 
subject      : /C=UK/O=eScience/OU=QueenMaryLondon/L=Computing/CN=ada lovelace/CN=proxy
issuer       : /C=UK/O=eScience/OU=QueenMaryLondon/L=Computing/CN=ada lovelace
identity     : /C=UK/O=eScience/OU=QueenMaryLondon/L=Computing/CN=ada lovelace
timeleft     : 23:53:59
DIRAC group  : gridpp_user
path         : /tmp/x509up_u501
username     : ada.lovelace
properties   : NormalUser
VOMS         : True
VOMS fqan    : ['/gridpp'] 

Proxies uploaded: 
 DN                                                          | Group       | Until (GMT) 
 /C=UK/O=eScience/OU=QueenMaryLondon/L=Computing/CN=ada lovelace | gridpp_user | 2016/03/24 14:40
```

If you get output that looks like the above, then it has all
worked.

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
You can check the status of your DIRAC proxy at any time
with the <code>dirac-proxy-info</code> command.
</td>
</tr>
</table>

## Configuring Ganga to use the DIRAC backend
There's just one more step required before you
can enjoy Grid running with Ganga -
you need to add the following to your
`~/.gangarc` configuration file:

```bash
[Configuration]
RUNTIME_PATH = GangaDirac

[LCG]
GLITE_SETUP = /cvmfs/ganga.cern.ch/dirac_ui/bashrc

[DIRAC]
DiracEnvSource = /cvmfs/ganga.cern.ch/dirac_ui/bashrc

[defaults_DiracProxy]
group = <dirac user group>
```
where `<dirac user group>` should be replaced by your
default VO (e.g. `gridpp_user`).
You can then re-start Ganga; it will now be ready to connect
to the DIRAC backend.

# Run your job on the Grid
Now you're ready to run your job on the Grid.
First, make a copy of the `local_job.py` script:
```bash
$ cd $WORKINGDIR
$ cp local_job.py dirac_job.py
$ vim dirac_job.py
```
All you need to do is add the line `j.backend=Dirac()`
before submitting. That's it. That's all there is to it.

```bash
$ cat dirac_job.py
j = Job()
j.name = "CERN@school_dirac_01"
j.application = Executable()
j.application.exe = File('run.sh')
j.application.args = ['B06-W0212/2014-04-02-150255/']
j.inputfiles = [ LocalFile('CERNatschool_backgroundrad_dataset.zip') ]
j.outputfiles = [ LocalFile('frames.json'), LocalFile('log_process-frames.log'), LocalFile('output_images.tar') ]
j.backend = Dirac()
j.submit()
```

(_Oh, you may want to change the job name too_.)

If all has gone to plan,
not only will you now be able to monitor your job
via your local Ganga instance (i.e. with the `jobs` command),
you can see it on the
[GridPP DIRAC web portal](http://dirac.gridpp.ac.uk).
Select _Jobs_ from the top-left menu below the URL bar,
then _Job Monitor_.

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
Job submission to the Grid is not an instant process -
a bit annoying when you're submitting one or two test jobs
(which is why local testing wit Ganga is great!),
but not such an issue with thousands of jobs.
You may wish to make a cup of tea, or do a bit of washing up.
</td>
</tr>
</table>

Once the job shows up as green in the web portal,
it's completed and you can retrieve the output exactly as before.

So there you go - your first _bona fida_ grid job. Note that:
* Once your Grid stuff/DIRAC configuration was done, all it
took to switch to Grid running was a single line of code.
* Thanks to CVMFS, you didn't have to do anything extra to
deploy your software to the Grid;
* You didn't need to care about where the job actually ran - Ganga and
DIRAC sorted that all for you.

There's only one more thing to look at now before we've covered
all of the Grid-bases - getting data on and off the Grid.
We'll look at that in the next section.
