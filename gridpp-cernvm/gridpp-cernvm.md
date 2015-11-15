#Creating a Grid UI with a GridPP CernVM

_For an overview of the process, see the [checklist](/checklist.html)_.

Your Grid User Interface (UI) is the means by which you will access the Grid.
For the purpose of getting you started quickly on the Grid with the
GridPP DIRAC instance, we will:

* Use the
<a href='https://www.scientificlinux.org/' target='_blank'>Scientific Linux 6</a>
(SL6) operating system;
* Perform most tasks via the command line using the terminal.

If you already have access to an account on an SL6 terminal, you can probably
skip this section.

If you don't,
or aren't quite sure what that last sentence even means,
don't worry.
We can create a Grid-ready UI from scratch on your own system using
_virtualisation_.
We will create a **Virtual Machine** (VM) that runs SL6 within whatever
operating system you happen to be using at the moment using the
<a href='http://cernvm.cern.ch/' target='_blank'>CernVM service</a>.
There are a number of reasons to do this:

1. Most of the Grid tools we'll use are compiled to run on SL6.
With a CernVM you'll be able to use them out of the box;
1. The standard Grid worker nodes you'll be using to run your software
on use SL6 machines. If your code runs on your CernVM, it will run
on the Gri.
1. We at GridPP will only have to support one operating system. If we're
singing from the same (virtual) hymn sheet, we'll be able to recreate your
problems and help you solve them more easily.

All you need to provide is the RAM and the hard disk space on your local machine.

Convinced? Good. Let's get started.

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
<a href='http://cernvm.cern.ch/portal/downloads' target='_blank'>here</a>.
It doesn't really matter which you use but we've had success with
<a href='http://download.virtualbox.org/virtualbox/4.3.12/VirtualBox-4.3.12-93733-Win.exe' target='_blank'>
this version of VirtualBox</a> (Windows 7).

> _This is the one bit that's a bit tricky for us to support - how you do this
> will depend on your local machine and its setup. Remember,
> search engines and
> <a href='http://stackoverflow.com/' target='_blank'>Stack Overflow</a>
> are your friends here_.

##Creating your CernVM
Depending on the virtualisation solution you picked (and got working)
above, download the baseline CernVM image file from
<a href='http://cernvm.cern.ch/portal/downloads' target='_blank'>here</a>.

> _At the time of writing (October 2015), the latest version was
> CernVM 3.5.1_.

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
<a href='https://cernvm-online.cern.ch/user/login' target='_blank'>here</a>.
If you don't have a CERN account, you can register
<a href='' target='https://cernvm-online.cern.ch/user/register'>here</a>.
1. **Visit the CernVM Marketplace**: This can be found
<a href='https://cernvm-online.cern.ch/market/list' target='_blank'>here</a>.
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

> With VirtualBox, for example, this is achieved using the
> _Shared Folders_ functionality.

Before proceeding, you should make sure that you can
access the parts of your local hard disk that contain
any software or data that you want to copy across and,
of course, your Grid certificate file.

##Getting help

This part of the process is one of the trickiest for us
to support as many different users will use different
host machines, virtualisation software, etc.
So, if you have any problems with any of the above steps,
please raise an issue on the
<a href='https://github.com/gridpp/user-guides/issues' target='_blank'>UserGuide GitHub Issues</a>
page and we'll try to help and update the documentation
accordingly. Thanks!

Now let's get on the Grid!
