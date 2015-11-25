#The CernVM: Create Your Own Virtual Grid Node
Before we get you on the Grid, we will first bring a little
(virtual) piece of the Grid to you.
The Grid consists of tens - possibly even hundreds - of thousands
of computing cores that power the Grid's **worker nodes**.

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
A <strong>Worker Node</strong> (WN) is the atomic unit of
Grid computing, representing a point within the Grid where
useful work - jobs - are carried at the behest of the Grid user
who submitted them.
</td>
</tr>
</table>

To give you a taste of the Grid before actually getting on the Grid,
we will create a **Virtual Machine** (VM)
that will, essentially, act like a Grid Worker Node (WN)
within whatever
operating system you happen to be using at the moment.
We will do this using the
<a href='http://cernvm.cern.ch/' target='_blank'>CernVM service</a>,
and create a guest CernVM on your host system.
There are a number of reasons to do this:

1. Most of the Grid tools we will use are compiled to run on
Scientific Linux 6;
With a CernVM you'll be able to use them out of the box;
1. The standard Grid Worker Nodes you'll be using to run your software
on use SL6 machines. If your code runs on your CernVM, it will run
on the Grid;
1. The CernVM can also act as a pre-built Grid User Interface (UI) that will give
you all the tools you need (e.g. a command line terminal, text editors, etc.)
to get the most out of the Grid;
1. What's more, if everyone uses the CernVM as their Grid UI,
we at GridPP will only have to support one operating system
(i.e. the SL6 supplied with the CernVM).
If we're singing from the same (virtual) hymn sheet, we'll be able to recreate your
problems and help you solve them more easily.

All you need to provide is the RAM and the hard disk space on your local host machine.

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
If you already have access to a user account on an SL6 terminal,
for example on a university computing cluster,
you can probably skip this section.
</td>
</tr>
</table>

##An overview of the process

To create and configure a CernVM that will meet our needs, you will need to:

1. Install some virtualisation software on your host machine;
1. Download the appropriate CernVM Virtual Machine baseline image from the
<a href='http://cernvm.cern.ch/' target='_blank'>CernVM service</a>;
1. Create a new guest CernVM using the CernVM image;
1. Configure the guest CernVM so that it has access to the host hard disk;
1. Configure the CernVM for Grid use by applying the GridPP _contextualisation_.

Let's look at each of these stages in a bit more detail.

##The virtualisation software
You can find a list of compatible virtualisation software solutions
on the CernVM image download page
[here](http://cernvm.cern.ch/portal/downloads).
It doesn't really matter which you use but we've had success with
[this version of VirtualBox](http://download.virtualbox.org/virtualbox/4.3.12/VirtualBox-4.3.12-93733-Win.exe)
(Windows 7).

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
This is the one bit that's a bit tricky for us to support - how you do this
will depend on your local machine and its setup. Remember,
search engines and
<a href='http://stackoverflow.com/' target='_blank'>StackOverflow</a>
are your friends here.
</td>
</tr>
</table>

##Creating your CernVM
Depending on the virtualisation solution you picked (and got working)
above, download the baseline CernVM image file from
<a href='http://cernvm.cern.ch/portal/downloads' target='_blank'>here</a>.

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
At the time of writing (October 2015), the latest version was
CernVM 3.5.1.
</td>
</tr>
</table>

Then use your virtualisation software to create a new VM from the
downloaded image. You should be able to find instructions for
how to do this from your virtualisation software provider.
Use as much RAM as you can spare (up to about half of your
host machine's total RAM) and use a virtual hard disk
of about 30 GB.

Once you have created your CernVM, but _before you start it_,
you will need setup the _contextualisation_ for your CernVM.

##Contextualising your CernVM
The CernVM service offers the ability to contextualise a CernVM
with pre-defined settings, environment variables, etc.
that are put in place when the CernVM is first booted.
This is known as _pairing_ the VM.
You can create your own contextuallisations,
but it is also possible for individuals to create public contexts
(e.g. for LHC experiments, open data initiatives, etc.)
that anyone can use.

We have created such a context for GridPP.
You can use it to get going with the Grid.
Importantly, you do not need a CERN account to do this,
so it is possible for anyone with a grid certificate to use it!

To pair your local CernVM with the GridPP context:

1. **Log in to the CernVM service**: You can do this
[here](https://cernvm-online.cern.ch/user/login).
If you don't have a CERN account, you can register
[here](https://cernvm-online.cern.ch/user/register).
1. **Visit the CernVM Marketplace**: This can be found
[here](https://cernvm-online.cern.ch/market/list).
1. **Select the GridPP CernVM context**:
Select _Experimental_ from the panel on the right,
and then click on the `gridpp-cernvm` context.
1. **Boot up your local CernVM**:
Once the boot process has finished,
you should be presented with a login prompt.
Don't enter anything yet.
1. **Pair with the GridPP context**:
Returning to the GridPP CernVM Marketplace,
click on the _Pair_ button on the panel on the right.
This will generate a six-figure PIN.
1. **Apply the context to your VM**:
Returning to your booted-up CernVM,
enter the PIN
(preceeded by a hash, as instructed at the login prompt).
The CernVM webpage will now update indicating the VM has been successfully paired.
Your VM will then be restarted and contextualised.
1. **Log in to your GridPP CernVM**:
Once the context has been applied to your CernVM,
you will be presented with a graphical
login screen (as opposed to the text login prompt).
Use the username `gridpp` and password `gridpp`
to log in to your CernVM.

And that's it! You now have a shiny new GridPP CernVM from which
you'll be able to access the Grid.

##One last thing: local hard disk access

Before we move on, it's important to note that
you will need to be able to access the hard disk of 
your host machine from that of your guest CernVM.
This is so that you can move any files that you need across
to the CernVM - most importantly, your Grid certificate file.

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
With VirtualBox, for example, this is achieved using the
Shared Folders functionality.
</td>
</tr>
</table>

Before proceeding, you should make sure that you can
access the parts of your local hard disk that contain
any software or data that you want to copy across.
