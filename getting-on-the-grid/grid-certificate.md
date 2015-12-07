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
[UK e-science Certificate Authority](http://ngs.ac.uk/ukca).
To start the process, you need to choose a web browser
that you will have consistent access to.
We recommend Firefox as this process has been tested
and confirmed to work with Firefox on most Operating Systems.
This is because you need to use the same system for both requesting your
certificate and retrieving it when it is ready.


<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
Do <strong>not</strong> use a temporary login anywhere when requesting a
grid certificate.
</td>
</tr>
</table>

Using your browser of choice visit
[this page](https://portal.ca.grid-support.ac.uk/caportal/)
and select the _Request New User Certificate_ option.
This almost goes without saying, but
make sure you supply a **valid email address** which you can access.
You will also be asked to do things like supply a PIN and
passwords that you will need later on, so **make sure you
write everything down**!
<!--, then choose
'User Certificate', fill in your personal details
(using your departmental email address) and select the appropriate
registration authority (RA) for your site.
-->

<table>
<tr>
<td align='center'><i class="fa fa-lightbulb-o" style='font-size:3em'></i></td>
<td>
You will need to select a
<strong>Registration Authority</strong> (RA) as part
of this process. If your institution does not have its own RA,
select the nearest on the drop-down menu. You will need to visit
the RA in person with some photographic identification, so don't
pick one that is too far away!
If no contact information is listed for a given RA,
they will almost certainly be retrievable using a Search Engine
of Your Choice or via their department's webpage. They will
be delighted to hear from you!
</td>
</tr>
</table>

Further instructions will then be emailed to you at the email address you
have supplied during the registration process.
Once that has happened you should get a further email from someone
at the RA asking you to visit them in person to complete the validation
process.

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
You may also be asked to supply a letter of recommendation
(or, rather, an email from a suitable authority)
explaining why you need to use the grid
and with whom you will be working.
If you are unsure about who to ask for this, please
<a href#'https://www.gridpp.ac.uk/contact' target='_blank'>contact us</a>
and we should be able to help you out.
</td>
</tr>
</table>

##Installing your grid certificate in your web browser

Assuming all has gone to plan,
you should receive a confirmation email with a link that will
let you download your grid certificate file and install it in
your browser.
You will now be able to export and backup your grid certificate
using your browser's certificate management functionality.
This process will vary from browser to browser and
from OS to OS, so consult the
[UK CA documentation](http://www.ngs.ac.uk/ukca/certificates)
if in doubt.

Congratulations - now you can be identified on the grid,
you're ready to
[join a Virtual Organisation](joining-a-vo.md).
