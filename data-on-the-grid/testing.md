#Putting Data on the Grid - Testing
* **Accessing data on a GridPP Storage Element (SE)**:
If everything is setup correctly, the following commands should
result in the output below:

```bash
$ cd ~
$ mkdir tmp
$ cd tmp
$ dirac-dms-get-file LFN:/gridpp/userguide/WELCOME.md
{'Failed': {},
 'Successful': {'/gridpp/userguide/WELCOME.md': '/home/alovelace/tmp/WELCOME.md'}}
$ cat WELCOME.md
#Welcome to GridPP!

It looks like your download has worked. Congratulations! 
```

_You should have been able to follow everything else in the
previous subsections too, of course - but much of the input
and output will depend on your username, VO, etc. - the real
test come when you start putting data in your own user area
in the [next section](../example-workflow-grid-data/example-workflow-grid-data.md)!_
