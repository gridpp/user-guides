#First steps with the Grid

So, you've got a working Grid UI up and running -
either using a GridPP CernVM on your local machine,
or on an account provided by your university cluster,
or some other way.
Great stuff.
Now it's time to take your first steps with the Grid
using your Grid certificate.
You do have a Grid certificate, right?

##Moving your Grid certificate to your UI
The first thing to do is move your Grid certificate
(the one you got after following the instructions
[here](../grid-certificate/grid-certificate.md))
to the `~/.globus/` directory in your home folder.

On a GridPP CernVM, the process would look something like this
(assuming your Grid certificate was saved in the `grid` directory
of the folder named _Home_ that you had enabled as a
_Shared Folder_ from your local machine):

```bash
[gridpp@localhost ~]$ pwd
/home/gridpp
[gridpp@localhost ~]$ mkdir .globus
[gridpp@localhost ~]$ cp /media/sf_Home/grid/my-certificate.p12 ./.globus/.
```

> _As you have moved your personal Grid certificate file
> to your CernVM,
> you should change the password of the `gridpp` account so
> that no-one else can use it. This can be done in the standard
> UNIX way with the `passwd` command_.

##Converting your Grid certificate
In order to use your Grid certificate,
you need to convert them into separate certificate and key files.
Don't worry, this straightforward enough to do with the following
commands:
```bash
[gridpp@localhost ~]$ cd ~/.globus
[gridpp@localhost ~]$ openssl pkcs12 -in [your-cert-file].p12 -clcerts -nokeys -out usercert.pem
Enter Import Password:
MAC verified OK
[gridpp@localhost ~]$ openssl pkcs12 -in [your-cert-file].p12 -nocerts -out userkey.pem
Enter Import Password:
MAC verified OK
Enter PEM pass phrase:
Verifying - Enter PEM pass phrase:
[gridpp@localhost ~]$ chmod 400 userkey.pem
[gridpp@localhost ~]$ chmod 600 usercert.pem
```
where the last two commands change the file permission settings.

##Cloning the GridPP Setup repository

Next there are a few setup files that we've put in a GitHub
repository for you to clone and run.

> _Note: ultimately this may be replaced with some clever
> contextualisation scripting, but for now it's easier
> to work with a GitHub repository..._

```bash
[gridpp@localhost ~]$ cd ~
[gridpp@localhost ~]$ git clone https://github.com/gridpp/gridpp-setup.git
[gridpp@localhost ~]$ cd gridpp-setup
[gridpp@localhost ~]$ . setup.sh
[gridpp@localhost ~] cd ~
```

##Generating a proxy

And now it's the moment you've been waiting for - the first
chance to interact with the Grid via your Grid certificate.
We'll generate a **proxy** - a temporary file that gives you
permission to work with Grid resources - via the command line
with the following command:

```bash
[gridpp@localhost ~] voms-proxy-init -dont-verify-ac --voms gridpp
Enter GRID pass phrase:
[Some output]
Creating proxy............... Done

Your proxy is valid until [date]
```

> _Note that this assumes you are a member of the `gridpp` VO.
> If you are not, replace `gridpp` with whichever VO you
> joined in the [Joining a VO](../joining-a-vo/joining-a-vo.md)
> section_.

Don't worry about the details too much for now - what matters
is that now, in principle, you have permission to use Grid
resources for the next 12 hours.
Now that's all very well, but we want to do something _useful_
with the Grid.

Let's go back to DIRAC.
