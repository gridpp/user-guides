#Troubleshooting
This section contains brief notes on specific problems users have
encountered when working on specific systems,
generally raised via the
[GitHub Issues page](http://github.com/gridpp/user-guides/issues).

##Ganga
_Ganga isn't working._

If you're having problems with Ganga, the best thing to do is to
[raise an issue](https://github.com/ganga-devs/ganga/issues)
with the Ganga dev team through the
[GitHub repository](https://github.com/ganga-devs/ganga/).
At the time of writing,
we've been using Ganga version 6.3.1 - but as Ganga is under
active development this may change so you may want to
[watch the repository too](https://github.com/ganga-devs/ganga).

_Ganga throws errors relating to not being able lock files._

If the file system your cluster is based on can't handle
(or hasn't been set up to allow)
file locks, which Ganga uses.
If your home directory is on such a file system
(e.g. NFS),
files in your `~/gangadir` won't be lockable and Ganga won't work.
Assuming your cluster can't be reconfigured, the simplest thing to
do is change the location of your `gangadir` to somewhere that
can handle file locks, such as a scratch directory on the cluster.
To do this, set the `gangadir` option in `~/.gangarc` to something like:

```bash
gangadir = /scratch/alovelace/gangadir
```

and restart Ganga in the usual way.

_My problem isn't listed here and search engines aren't helping either._

Raise an issue on the
[GitHub issues page](http://github.com/gridpp/user-guides/issues)
and we'll see if we can help!

Good luck!
