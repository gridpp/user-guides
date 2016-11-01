# Preparing your grid certificate
Ganga will assume that your grid certificate is in a certain
location and in a certain format in order to use it.
Your grid certificate therefore needs to be moved and
prepared accordingly - which you can do by following the
instructions below.

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

And that's it! You're now ready to use GridPP DIRAC
with Ganga. It may have seemed like a lot of work,
but hopefully the
[next section](../example-workflow-grid/example-workflow-grid.md)
will demonstrate
it will all have been worth it.
