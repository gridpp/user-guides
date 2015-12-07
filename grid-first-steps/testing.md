#First steps with the Grid - Testing

* **Moving your Grid certificate file to the `.globus` directory**:
The following commands produce the following output:
```bash
$ cd ~
$ ls .globus/
[certificate name].p12
```
* **Converting your Grid certificate**:
The following commands produce the following output:
```bash
$ cd ~
$ ls .globus/
[certificate name].p12 usercert.pem userkey.pem
```

* **Setting the file permissions on your certificate and key file**:
The following commands produce something similar to the following output:
```bash
$ cd ~
$ ls -l .globus/
total 12
-rwxrwx--- 1 gridpp gridpp 2906 Oct  2 20:16 [certificate name].p12
-rw------- 1 gridpp gridpp 2022 Oct  2 20:32 usercert.pem
-r-------- 1 gridpp gridpp 1993 Oct  2 20:34 userkey.pem
```

* **Cloning and setting up the `gridpp-setup` repository**:
After cloning the `gridpp-setup` repository and running the
`setup.sh` script therein,
the following commands should produce the following output:
```bash
$ cd ~
$ ls gridpp-setup/
README.md  cvmfscfg  setup.sh  vomscfg
$ echo $VOMS_USERCONF 
/home/gridpp/gridpp-setup/vomscfg/vomses
```

* **Generating a proxy**:
After generating a proxy, you can use the `voms-proxy-info`
command to generate something similar to the following output:
```bash
$ voms-proxy-info
subject   : /C=UK/O=eScience/OU=QueenMaryLondon/L=Computing/CN=ada lovelace/CN=proxy
issuer    : /C=UK/O=eScience/OU=QueenMaryLondon/L=Computing/CN=ada lovelace
identity  : /C=UK/O=eScience/OU=QueenMaryLondon/L=Computing/CN=ada lovelace
type      : proxy
strength  : 1024 bits
path      : /tmp/x509up_u501
timeleft  : 11:59:58
```
