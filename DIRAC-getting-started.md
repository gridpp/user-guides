This guide presents a series of checklists to work through - with tests - to get you started with the Imperial DIRAC instance. If you have any problems, or the steps aren't clear, please raise <a href="https://github.com/gridpp/user-guides/issues" target="_blank">an issue</a>.

##First steps
* I have a <a href="https://www.gridpp.ac.uk/wiki/Grid_user_crash_course#Getting_a_grid_certificate" target="_blank">grid certificate</a>;
* I have <a href="http://ngs.ac.uk/ukca/certificates/certimport" target="_blank">installed my grid certificate in my browser</a>;
* I have joined a VO;
* I have accessed the <a href="https://dirac.gridpp.ac.uk" target="_blank">Imperial DIRAC server</a>;
* I have joined the <a href="https://mailman.ic.ac.uk/mailman/listinfo/gridpp-dirac-users" target="_blank">Imperial DIRAC mailing list</a>.

##First steps - testing

* **Viewing your certificate details**: visit <a href="https://portal.ca.grid-support.ac.uk/caportal/cert_owner" target="_blank">this website</a> with your browser. You should see your grid certificate details displayed;
* **Accessing the Imperial DIRAC server**: access https://dirac.gridpp.ac.uk with your browser. If your grid certificate has been successfully installed in your browser, your browser should ask you to identify yourself with the certificate in question. You will then see the Imperial DIRAC server homepage. Check the bottom right-hand corner - if you can only see _Visitor_ and **not** your username and DN, you are (or rather, your certificate is) not registered with the Imperial DIRAC server
* - please contact [mailto:lcg-site-admin@imperial.ac.uk Imperial Dirac Support]. Note that there is a couple of hours (< 24) delay after joining a VO, before the dirac server recognizes you.
* **Joining the Imperial DIRAC mailing list**: once you have subscribed, you should be able to view the <a href="https://mailman.ic.ac.uk/mailman/roster/gridpp-dirac-users" target="_blank">subscribers list</a> from the <a href="https://mailman.ic.ac.uk/mailman/listinfo/gridpp-dirac-users" target="_blank">list homepage</a> and see that you're on it.


##Your Virtual Organisation
* I have <a href="https://www.gridpp.ac.uk/wiki/Grid_user_crash_course#Joining_a_VO" target="_blank">joined a supported Virtual Organisation</a> (VO);
* I have checked that my VO is supported by the <a href="https://dirac.grid.hep.ph.ic.ac.uk:8443" target="_blank"> Imperial DIRAC server</a>;
* I have accessed the <a href="https://dirac.grid.hep.ph.ic.ac.uk:8443" target="_blank">Imperial DIRAC server</a> as a member of my VO.

##Your Virtual Organisation - testing
* **Joining a VO**: You should receive a confirmation email with the subject _[VOMS Admin] Your vo membership request for VO [VO name] has been approved._ - where _[VO name]_ is the name of the VO - within 24 hours. You may be asked to confirm the request - **_make sure you don't accidentally cancel the request_**.
* **Accessing the Imperial DIRAC server as a VO member**: access https://dirac.gridpp.ac.uk with your browser. Click on the drop-down menu displaying _Visitor_. You should be able to select your VO by clicking on the name. If not, contact <a href="mailto:lcg-site-admin@imperial.ac.uk">lcg-site-admin@imperial.ac.uk</a>.


##DIRAC client installation
* I have <a href="https://www.gridpp.ac.uk/wiki/Grid_user_crash_course#Converting_your_grid_certificate" target="_blank">converted my grid certificate</a> into a **certificate file** and **key file** and put these in my `~/.globus` directory;
* I can communicate with the DIRAC configuration server from my local system;
* I have installed a DIRAC client on my local system (following the instructions <a href="https://www.gridpp.ac.uk/wiki/Quick_Guide_to_Dirac#Dirac_client_installation" target="_blank">here</a>);
* I have generated a proxy with my grid certificate (following the instructions <a href="https://www.gridpp.ac.uk/wiki/Quick_Guide_to_Dirac#Create_a_proxy_for_a_community" target="_blank">here</a>).

##DIRAC client installation - testing
* **Grid certificate conversion and installation**: when logged on to your local system, <code>ls ~/.globus</code> should return <code>usercert.pem</code> and <code>userkey.pem</code>;
* **Contacting the configuration server**: when logged on to your local system, <code>nc -v 146.179.247.169 9135</code> should work. If not, contact your system administrator and/or check your firewall settings.
* **DIRAC client installation**: the installation procedure should run with no error messages. Upon sourcing <code>. $DIRACDIR/bashrc</code>, you should be able to run (and tab-complete) the <code>dirac-*</code> commands;
* **Proxy generation with DIRAC**: if the installation has been successful, upon entering the DIRAC proxy generation command:

```bash
$ dirac-proxy-init -g northgrid_user -M
```

you should asked to enter your certificate password and then receive a message similar to the following (the values in square brackets will vary):

```
Generating proxy... 
Enter Certificate password:
Uploading proxy for gridpp_user... 

Proxy generated: 
subject      : [your grid certificate DN]
issuer       : [your grid certificate DN]
identity     : [your grid certificate DN]
timeleft     : [reminaing time]
DIRAC group  : northgrid_user
path         : /tmp/x509up_u500
username     : [your username]
properties   : NormalUser
VOMS         : True
VOMS fqan    : ['/[VO name]'] 

Proxies uploaded: 
 DN                                                           | Group             | Until (GMT) 
 [your DN]                                                    | northgrid_user    | [time left on proxy] 
```

##The official DIRAC tutorials

The "official" DIRAC tutorials can be found on their GitHub wiki <a href="https://github.com/DIRACGrid/DIRAC/wiki/DIRAC-Tutorials" target="_blank">here</a>. Tutorials 1-3 are covered by the steps above, so we will start at number 4.

Please note that these tutorials are based on a different DIRAC instance, and so details like Storage Elements will differ from those available on the Imperial DIRAC instance. Please ask the <a href="mailto:lcg-site-admin@imperial.ac.uk">Imperial DIRAC support team</a> about which SEs are supported by your VO and adjust the commands accordingly.

###Tutorial 4. Job management basics
After following the <a href="https://github.com/DIRACGrid/DIRAC/wiki/JobManagement" target="_blank">tutorial</a>, I can:
* Submit a simple job;
* Query the status of my simple job;
* Retrieve the output of my simple job;
* Submit and retrieve the output from a job that runs a custom script using the <code>InputSandbox</code>.

###Tutorial 5. Data management basics
After following the <a href="https://github.com/DIRACGrid/DIRAC/wiki/DataManagement" target="_blank">tutorial</a>, I can:
* List the Storage Elements (SEs) available to me through my VO;
* Upload a local file to my VO's user area at <code>/$VO_NAME/user/$SUERNAME_FIRST_INITIAL/$USERNAME/</code>;
* Download the file from the SE to <code>$WORKINGDIR/tmp</code>;
* Create a replica of the file on another SE;
* Remove the replica of the file;
* Remove the file from the grid.

###Tutorial 6. File catalog basics
After following the <a href="https://github.com/DIRACGrid/DIRAC/wiki/FileCatalog" target="_blank">tutorial</a>, I can:
* Start the DIRAC File Catalog interface;
* Move to my user directory in the DFC, <code>/$VO_NAME/user/$USERNAME_FIRST_INITIAL/$USERNAME/</code>;
* Create a new test directory in my user directory;
* Upload a local file to this new directory;
* Get the size of the file from it's Logical File Name (LFN);
* Remove the file;
* Remove the test directory;
* Retrieve my DIRAC identity information.

##The official DIRAC tutorials - testing

###Tutorial 4. Job management basics - testing

* **Simple job submission**: your simple job - performing <code>ls -ltr</code> on the worker node - should run successfully. You can retrieve the output using <code>dirac-wms-job-get-output [job ID]</code>, and view the <code>$WORKINGDIR/[job ID]/StdOut</code> file.
* **Submitting a script with the InputSandbox**: your job runs the script uploaded with the <code>InputSandbox</code> runs successfully. You can retrieve the job output and view any files that you requested be retrieved with <code>OutputSandbox</code> in the <code>$WORKINGDIR/[job ID]</code> directory.

###Tutorial 5. Data management basics - testing
* **File upload, download and removal**: you can perform the steps listed above without generating any errors.

###Tutorial 6. File catalog basics - testing
* **File upload, download and removal with the File Catalog Client**: you can perform the steps listed above without generating any errors.
