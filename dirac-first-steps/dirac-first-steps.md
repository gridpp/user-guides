#First steps with DIRAC

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
As a new user, you can register to use the GridPP DIRAC instance
as a member of the `gridpp` VO or one of the Regional VOs.
This will allow you to test out various bits of grid functionality
to determine if grid computing will meet your needs and the needs
of your users.

To register, simply email the
<a href="mailto:lcg-site-admin@imperial.ac.uk" target="_blank">GridPP DIRAC Support Team</a>
with your grid certificate DN
(you can find this out by accessing
<a href="https://portal.ca.grid-support.ac.uk/caportal/cert_owner" target="_blank">this website</a>)
and the VOs you wish to use with the GridPP DIRAC instance.

A typical registration request email should look like this:

```
To:   lcg-site-admin@imperial.ac.uk
From: a.lovelace@london.ac.uk
Subject: GridPP DIRAC registration

Dear GridPP DIRAC team,

I would like to register with GridPP DIRAC. Please could you arrange this for me?

My certificate DN is:

/C=UK/O=eScience/OU=UniOfLondon/L=Computing/CN=ada lovelace

and I would like to be registered with the following VOs:

vo.londongrid.ac.uk
vo.analytical-engine.ac.uk

Many thanks in advance, Ada
```

All being well the GridPP DIRAC team should respond within 24 hours
to inform you that you have been successfully registered.
You can test the success of the registration by following the
steps [here](testing.md).

Once registered with DIRAC you will be able to interact with the
Grid via the GridPP DIRAC web portal at
<a href='https://dirac.gridpp.ac.uk' target='_blank'>https://dirac.gridpp.ac.uk</a>.
However, to harness the true power of GridPP's resources you
will probably need a User Interface (UI) with access to DIRAC's
command line and scripting functionality.
We'll look at this in the next few sections.
