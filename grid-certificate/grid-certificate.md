#Your Grid certificate

Your grid certificate is your passport to the grid.
It will give you access to the vast array of computational resources that
GridPP (and the wLCG) has to offer.
As such, getting a grid certificate is an understandably non-trivial,
multi-step process.
For example, you will need to identify yourself to your local
Registration Authority (RA) so that the grid knows who you are.

In concrete terms, a grid certificate is a .p12 file
(i.e. a pkcs12 web browser certificate file)
that you will later convert into a _user key_ file
and a _user certificate_ file.
Encoded according to the X.509 standard,
these are used by the grid to confirm
who are you are and so give you access to grid resources.

##Requesting a grid certificate

Grid certificates in the UK are managed by the
<a href="http://ngs.ac.uk/ukca" target="_blank">UK e-science Certificate Authority</a>.
To start the process, you need to choose a web browser (e.g. Firefox)
that you will have consistent access to.
This is because you need to use the same system for both requesting your
certificate and retrieving it when it is ready.

> _Do **not** use a temporary login anywhere when requesting a
> grid certificate_.

Using your browser of choice visit
<a href="https://https://portal.ca.grid-support.ac.uk/caportal/" target="_blank">this page</a>
and select the _Request New User Certificate_ option.
<!--, then choose
'User Certificate', fill in your personal details
(using your departmental email address) and select the appropriate
registration authority (RA) for your site.
-->

> _You will need to select a **Registration Authority** (RA) as part
> of this process. If your institution does not have its own RA,
> select the nearest on the drop-down menu. You will need to visit
> the RA in person with some photographic identification, so don't
> pick one that is too far away!_

Further instructions will then be emailed to you at the email address you
have supplied.
Once that has happened you should get a further email from someone
at the RA asking you to visit them in person to complete the validation
process.

##Installing your grid certificate in your web browser

Assuming all has gone to plan,
you should receive a confirmation email with a link that will
let you download your grid certificate file and install it in
your browser.
You will now be able to export and backup your grid certificate
using your browser's certificate management functionality.

Congratulations - now you can be identified on the grid,
you're ready to join a Virtual Organisation.
