# First steps: Hello World(s)! - Testing

* **Running Ganga from the command line**: if you have successfully
run Ganga, you should now have the following in your `$HOME` directory:
```bash
$ cd $HOME
$ ls ~/.gangarc
/home/alovelace/.gangarc
$ ls ~/gangadir
repository  shared  thread_trace.html  workspace
```

* **Looking at the output from local Ganga jobs**: assuming you
haven't removed them (you can always re-run them again if you have),
you should be able to find the actual output files from your jobs
in your `gangadir`. So for user `alovelace`'s job 0, the output
can be found in:
```bash
$ ls $HOME/gangadir/workspace/alovelace/LocalXML/0/output/
__jobstatus__ stdout stderr __syslog__
```
You should see something similar (and you can look at the output
in `stdout` directly if you like!).
