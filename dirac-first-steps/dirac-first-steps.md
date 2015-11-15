#First steps with DIRAC

_For an overview of the process, see the [checklist](/checklist.html)_.

There are many ways of accessing and using grid resources.
Larger organisations - such as the four LHC experiments - 
have developed their own frameworks, architectures and mechanisms
to enable their members to run jobs and access experimental data.

One such framework - DIRAC - is used by LHCb, but also
many other grid projects, to manage grid jobs and storage.
You can read more about
DIRAC (Distributed Infrastructure with Remote Agent Control)
<a href="http://diracgrid.org/" target="_blank">here</a>,
but for our purposes all you need to know for now is that
DIRAC provides a way for you to access grid resources
without worrying too much about what's going on
behind the scenes.

##The GridPP DIRAC instance

The Imperial College London GridPP Resource Centre (RC) hosts an
instance of DIRAC on behalf of GridPP.
The Imperial DIRAC instance is is capable of serving multiple VOs,
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
<a href='https://dirac.gridpp.ac.uk' target='_blank'>https://dirac.gridpp.ac.uk</a>.
When you access the portal, you should see yourself listed as
a **Visitor** in drop-down menu in the bottom-right corner of the browser.
Once you have joined one or more DIRAC-supported Virtual Organisations,
you will be able to select which VO you use DIRAC as
using this drop-down menu.

> You should also join the GridPP DIRAC mailing list
> to keep informed of the latest developments
> and receive notices of any downtime.
> You can join the mailing list
> <a href='https://mailman.ic.ac.uk/mailman/listinfo/gridpp-dirac-users' target='_blank'>here</a>.

So you've accessed the GridPP DIRAC web portal. Congratulations!
However, to harness the true power of GridPP's resources you
will probably need a User Interface (UI) with access to DIRAC's
command line and scripting functionality.
We'll look at this in the next few sections.
