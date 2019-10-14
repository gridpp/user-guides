#The GridPP UserGuide 

Welcome to the _GridPP UserGuide_.
The [GridPP Collaboration](https://www.gridpp.ac.uk)
is a community of particle physicists
and computer scientists based in the United Kingdom and at
[CERN](http://cern.ch).
It supports tens of thousands of CPU cores
and petabytes of data storage across the UK which,
amongst other things,
played a crucial role in the 
discovery of the Higgs boson at
[CERN](http://cern.ch)'s
Large Hadron Collider.
The aim of this document
is to help new users - like you -
join this community and access these resources
to make a difference to the world
beyond the realm of particle physics. 

So, if you have a data-intensive problem that could
be solved using large-scale distributed computing,
read on!

##Who is this guide for?
This guide is primarily aimed at people
from user communities that have not previously
engaged with grid
(a.k.a. distributed computing)
technology. You could be:

* a researcher from a UK institution with a problem
that could be solved by the application of
thousands of computers running software in parallel
over large, structured data sets;
* a student from the UK
who would benefit from being able to access
computing and data storage resources that
your own institution cannot provide (i.e. your school);
* a tech entrepreneur from a start-up or
Small-to-Medium Enterprise (SME) who would like to
test how your software or app scales to thousands
of machines for zero cost and minimal risk.

The _GridPP UserGuide_ isn't really aimed at:

* Members of scientific collaborations who already have
a grid presence and infrastructure in place
(e.g. CMS, ATLAS, SNO++, T2K);
* Users from outside of the UK - you should refer to
your own country's National Grid Initiative (NGI) to
find out about the best way of getting on the grid,

although it may serve as a useful reference
for members of these communities.

<table>
<tr>
<td align='center'><i class="fa fa-warning" style='font-size:3em'></i></td>
<td>
<em>While every effort has been made to cover as many
bases as possible, some computing knowledge is
assumed. You can read more about what you might need to know  in the
<a href='before-we-begin/before-we-begin.html'>prerequisites</a>
section</em>.
</td>
</tr>
</table>

##What do I do next?
You should read the
[Before We Begin](before-we-begin/before-we-begin.html)
section to go over the
[prerequisites](before-we-begin/prerequisites.html),
the
[UserGuide conventions](before-we-begin/conventions.html),
and how to get
[help and support](before-we-begin/getting-help.html)
from the GridPP community.
If you do not have access to a **Grid User Interface** (UI)
(or don't know what that means),
you should then look at creating one following the
instructions
[here](gridpp-cernvm/gridpp-cernvm.html).
Then it's simply a case of getting a **grid certificate**,
joining a **Virtual Organisation** (VO), and
getting on the Grid!

<table>
<tr>
<td align='center'><i class="fa fa-info-circle" style='font-size:3em'></i></td>
<td>
<em>Don't worry, we'll explain all of those terms
as we go along - mostly using little information boxes like this one.
For now, though, you can start
<a href='before-we-begin/before-we-begin.html'>here</a></em>.
</td>
</tr>
</table>

##Acknowledgements
This work was supported by
the UK's
[Science and Technology Facilities Council](http://www.stfc.ac.uk)
(STFC) via the GridPP Collaboration.
The author would like to thank
GridPP Collaboration members
Steve Jones (Liverpool) and Steve Lloyd (QMUL),
as well as the students of the
[Simon Langton Grammar School for Boys](http://www.thelangton.org.uk),
for providing invaluable feedback on the initial drafts of the
_GridPP UserGuide_.
Much inspiration for the structure and philosophy of the
_GridPP UserGuide_ has been drawn from Michael Hartl's
_[Ruby on Rails Tutorial](https://ww.railstutorial.org)_ - an
excellent read (even if you're not particularly fussed about
Ruby on Rails). We are also grateful to
[GitHub](http://github.com) for our
[Organizational Repository](http://github.com/gridpp) - thanks!

##About the author
Tom Whyntie is Public Engagement Fellow at the
[School of Physics & Astronomy](http://ph.qmul.ac.uk),
[Queen Mary University of London](http://www.qmul.ac.uk).
He is supported by the UK's
[Science and Technology Facility Council](http://www.stfc.ac.uk) (STFC)
through their
[Public Engagement Fellowship](http://www.stfc.ac.uk/funding/fellowships/public-engagement-fellowships/public-engagement-fellows/)
programme and through the
[GridPP Project](https://www.gridpp.ac.uk).
Having used the Worldwide LHC Computing Grid (WLCG) extensively
during his time on the
[Compact Muon Solenoid](http://cms.web.cern.ch/)
(CMS) experiment at
[CERN](http://cern.ch)'s Large Hadron Collider,
Tom works as part of the GridPP Community to
engage as many people as possible with the Grid
through GridPP's New User Engagement Programme.
He is also consultant scientist for the
[CERN@school programme](http://cernatschool.web.cern.ch),
Scientific Officer for the
[Institute for Research in Schools](http://researchinschools.org),
and a member of the
[MoEDAL Collaboration](http://moedal.web.cern.ch).

You can follow Tom on Twitter [here](http://twitter.com/twhyntie)
and on GitHub [here](http:github.com/twhyntie).

##Copyright and license

<a rel='license' href='http://creativecommons.org/licenses/by-sa/4.0/'>
<img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" />
</a>

The _GridPP UserGuide_ is licensed under a
[Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
It is based on a work hosted at [https://github.com/gridpp/user-guides/](https://github.com/gridpp/user-guides/).
All source code in the _GridPP UserGuide_ is available jointly
under the
[MIT License](http://opensource.org/licenses/MIT)
and the
[Beerware License](http://people.freebsd.org/~phk/):

```
The MIT License

Copyright (c) 2015 The GridPP Collaboration

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.  IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
```

```
/*
 * ----------------------------------------------------------------------------
 * "THE BEERWARE LICENSE" (Revision 43):
 * Tom Whyntie wrote this code (unless otherwise credited).
 * As long as you retain this notice you
 * can do whatever you want with this stuff. If you meet him, and you think
 * this stuff is worth it, you can buy him a beer (or coffee) in return.
 * ----------------------------------------------------------------------------
 */
```
