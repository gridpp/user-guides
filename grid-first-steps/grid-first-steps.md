#First steps with the Grid

So, you've got a working Grid User Interface (UI) up and running -
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
[here](../getting-on-the-grid/grid-certificate.md))
to the `~/.globus/` directory in your home folder.

```bash
$ cd ~
$ pwd
[Your home directory.]
$ mkdir .globus
$ cp [The location of your certificate file.]/[Your certificate filename].p12 ./.globus/.
```

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
If you are using a CernVM and have moved your personal
Grid certificate file to it,
you should change the password of the <code>gridpp</code> account so
that no-one else can use it. This can be done in the standard
UNIX way with the <code>passwd</code> command.
</td>
</tr>
</table>

##Converting your Grid certificate
In order to use your Grid certificate,
you need to convert them into separate certificate and key files.
Don't worry, this straightforward enough to do with the following
commands:
```bash
$ cd ~/.globus
$ openssl pkcs12 -in [Your certificate filename.].p12 -clcerts -nokeys -out usercert.pem
Enter Import Password:
MAC verified OK
$ openssl pkcs12 -in [Your certificate filename.].p12 -nocerts -out userkey.pem
Enter Import Password:
MAC verified OK
Enter PEM pass phrase:
Verifying - Enter PEM pass phrase:
```

You will then need to change the file permission settings on
the two newly-generated files:

```bash
$ chmod 400 userkey.pem
$ chmod 600 usercert.pem
```

##Cloning the GridPP Setup repository

Next there are a few setup files that we've put in a GitHub
repository for you to clone and run.

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
Ultimately this step of the <em>UserGuide</em> may be replaced with some clever
virtual machine contextualisation scripting, but for now we'll work with
with a GitHub repository...
</td>
</tr>
</table>

```bash
$ cd ~
$ git clone https://github.com/gridpp/gridpp-setup.git
$ cd gridpp-setup
$ . setup.sh
$ cd ~
```

##Generating a proxy

And now it's the moment you've been waiting for - the first
chance to interact with the Grid via your Grid certificate.
We'll generate a **proxy** - a temporary file that gives you
permission to work with Grid resources - via the command line
with the following command:

```bash
$ voms-proxy-init --dont_verify_ac --voms gridpp
Enter GRID pass phrase:
[Some output]
Creating proxy............... Done

Your proxy is valid until [date]
```

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
Note that this assumes you are a member of the <code>gridpp</code> VO.
If you are not, replace <code>gridpp</code> with whichever VO you
joined in the
<a href='../getting-on-the-grid/joining-a-vo.md'>Joining a VO</a>
section.
</td>
</tr>
</table>

Don't worry about the details too much for now - what matters
is that now, in principle, you have permission to use Grid
resources for the next 12 hours.
That's all very well, but we want to do something _useful_
with the Grid. For that, we'll need GridPP DIRAC.
