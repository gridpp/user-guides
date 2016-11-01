#First steps with GridPP DIRAC

There are many ways of accessing and using grid resources.
Larger organisations - such as the four LHC experiments - 
have developed their own frameworks, architectures and mechanisms
to enable their members to run jobs and access experimental data.

One such framework - DIRAC - is used by LHCb, but also
many other grid projects, to manage grid jobs and storage.
You can read more about
DIRAC (Distributed Infrastructure with Remote Agent Control)
[here](http://diracgrid.org),
but for our purposes all you need to know for now is that
DIRAC provides a way for you to access grid resources
without worrying too much about what's going on
behind the scenes.

##The GridPP DIRAC instance

The Imperial College London GridPP Resource Centre (RC) hosts an
instance of DIRAC on behalf of GridPP.
The GridPP DIRAC instance is is capable of serving multiple VOs,
providing grid job and data management capabilities for smaller,
non-LHC user communities wishing to make use of GridPP resources.
As a new user, you are automatically registered with the
GridPP DIRAC instance and the Virtual Organisations you have
joined.
You can then test out various bits of grid functionality
to determine if grid computing will meet your needs and the needs
of your users.

You can interact with the
Grid via the GridPP DIRAC web portal at
[https://dirac.gridpp.ac.uk](https://dirac.gridpp.ac.uk).
When you access the portal, you should see yourself listed as
a **Visitor** in drop-down menu in the bottom-right corner of the browser.
Once you have joined one or more DIRAC-supported Virtual Organisations,
you will be able to select which VO you use DIRAC as
using this drop-down menu.

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
You should also join the GridPP DIRAC mailing list
to keep informed of the latest developments
and receive notices of any downtime.
You can join the mailing list
<a href='https://mailman.ic.ac.uk/mailman/listinfo/gridpp-dirac-users' target='_blank'>here</a>.
</td>
</tr>
</table>

So you've accessed the GridPP DIRAC web portal. Congratulations!
However, as discussed, we'll be using GridPP DIRAC via the Ganga interface.
In order to do that, you'll need to install your grid certificate on
your local machine - and the instructions for this are
[here](preparing-your-certificate.md).
