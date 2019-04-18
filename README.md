

<!-- <br /> -->
<!-- <p><span class="sidetitle">This document</span></p> -->
<!-- <a href="#license" title="Before we go on: licenses">Licenses</a> -->
<!-- <a href="#do" title="What the programs do">What?</a> -->
<!-- <a href="#why" title="Why record behavior using an HP48 calculator?">Why?</a> -->
<!-- <a href="#alternatives" title="Alternatives: Things I would do differently now">Alternatives</a> -->
<!-- <a href="#flow" title="Basic program flow">Flow</a> -->
<!-- <a href="#cmm" title="The C++ programs">C++ progr.</a> -->
<!-- <a href="#hp" title="The HP 48 programs">HP 48 progr.</a> -->

<!-- <br /> -->




<!-- <p><span class="sidetitle">BehHP48</span></p> -->
<!-- <a href="BehHP48-manual.html" title="Documentation for the HP 48 programs">Documentation</a> -->
<!-- <a href="#download" title="Download">Download</a> -->
<!-- <\!-- <a href="GPL.txt" title="GPL license (local copy)">GPL License (local)</a> -\-> -->
<!-- <\!-- <a href="http://www.gnu.org/licenses/licenses.html#GPL" title="GPL license (GNU site)">GPL License (GNU site)</a> -\-> -->
<!-- <a href="OriginalEmailHP48.html" title="Original email that got all going -->
<!-- (local)">History (local copy)</a> -->
<!-- <a href="http://segate.sunet.se/cgi-bin/wa?A2=ind9606&amp;L=ethology&amp;F=&amp;S=&amp;P=4352" -->
<!-- title="Original email that got all going">History</a> -->
<!-- </div> -->





<h1>Behavioral Recording with the HP 48 Calculator</h1>

<br />

<div id="licensesection">
<!-- Creative Commons License -->
<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/2.0/">
<img alt="Creative Commons License" src="../somerights20.gif" /></a><br />
<span class="license">This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/2.0/">Creative Commons License</a></span>.
<!-- /Creative Commons License -->

<!--

<rdf:RDF xmlns="http://web.resource.org/cc/"
xmlns:dc="http://purl.org/dc/elements/1.1/"
xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"> <Work rdf:about="">
<dc:title>Behavioral recording with the HP 48 calculator</dc:title>
<dc:date>1996, 2004</dc:date>
<dc:description>Comments about the BehHP48 bundle of programs
and issues about behavioral recording with handhelds</dc:description>
<dc:creator><Agent>
<dc:title>Ramón Díaz-Uriarte</dc:title>
</Agent></dc:creator>
<dc:rights><Agent>
<dc:title>Ramón Díaz-Uriarte</dc:title>
</Agent></dc:rights>
<dc:type
rdf:resource="http://purl.org/dc/dcmitype/Text"
/>
<license
rdf:resource="http://creativecommons.org/licenses/by-nc-sa/2.0/"
/>
</Work>

<License
rdf:about="http://creativecommons.org/licenses/by-nc-sa/2.0/">
<permits
rdf:resource="http://web.resource.org/cc/Reproduction"
/>
<permits
rdf:resource="http://web.resource.org/cc/Distribution"
/>
<requires
rdf:resource="http://web.resource.org/cc/Notice"
/>
<requires
rdf:resource="http://web.resource.org/cc/Attribution"
/>
<prohibits
rdf:resource="http://web.resource.org/cc/CommercialUse"
/>
<permits
rdf:resource="http://web.resource.org/cc/DerivativeWorks"
/>
<requires
rdf:resource="http://web.resource.org/cc/ShareAlike"
/>
</License>

</rdf:RDF>

-->
</div> 
<br />


These set of HP 48 and C++ programs
were used to record behavioral data (and help in the execution of
experiments) for the experiments with lizards on antipredator and aggressive
behavior reported in, for example, Díaz-Uriarte, 1999 ("Anti-predator behavior
changes following an aggressive encounter in the lizard <em>Tropidurus
hispidus</em>." <a name="antip.paper">Proceedings of the Royal Society of London, Series B, 266:
2457--2464</a> or
chapter 1 of <a href="http://bioinfo.cnio.es/~rdiaz/Thesis.RDiaz.pdf">my PhD thesis</a>). I show here only a set of programs (those used in the
first set of experiments reported in that paper), but many modifications, for
other experiments and observations, were used. Sure enough, it is trivial to
use the HP 48 just to record data (e.g, I used a lot to collect biometric
data on the lizards). I make this code available in the hope that it can be
of use for anybody else; all this code is distributed under the <a
href="http://www.gnu.org/licenses/licenses.html#GPL">GNU GPL</a> license (see below), so you you can modify it and rewrite
it to suit your needs. Note, however, that I am not in a position to solve
problems with the code, or help you customize it;  however, if you decide to
use it, I'd appreciate if you could let me know.

<h2><a name="license">Before we go on: licenses</a></h2>

<h3>Programs' license</h3>

<p>These programs (exp6, anq6, cl6, antipa.cpp, antipa.h, antipb.cpp,
antipb.h, antip20.h) are free software; you can redistribute them and/or modify  
    them under the terms of the GNU General Public License as published by  
    the Free Software Foundation; either version 2 of the License, or     
    (at your option) any later version.</p>                                   
                                                                          
   <p>These programs are distributed in the hope that they will be useful,        
   but WITHOUT ANY WARRANTY; without even the implied warranty of         
   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the          
   GNU General Public License for more details.</p>                           
                                                                          
   <p>A copy of the GNU General Public License is included in the bundle of
code. A copy can be obtained from the  Free Software             
  Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307,USA, or
from <a href="http://www.gnu.org/licenses/licenses.html#GPL">the GNU licenses' page</a>.</p> 
                                                                          

<h3>Programs' documentation license</h3>

The <a href="BehHP48-manual.html">"manual"</a> is under the
<a href="BehHP48-manual.html#SEC1">GNU Free Documentation License</a>.

<h3>This file's license</h3>
As mentioned above, this is licensed under a
<a href="http://creativecommons.org/licenses/by-nc-sa/2.0/">Creative Commons
license</a>, as most of the stuff in this site is.

<h3>Copyright</h3>
The code, manual, and this file 
are copyright © 1996, 2004, Ramón Díaz-Uriarte.



<h2><a name="do">What the programs do</a></h2>
These set of HP 48 and C++ programs are used to record behavioral data (and
help in the execution of the experiment) for the experiments with lizards on
antipredator and aggressive behavior reported in, for example, Díaz-Uriarte,
programs (those used in the first set of experiments reported in that paper),
1999 (the Proc Roy Soc London paper, mentioned <a href="#antip.paper">above</a>). I show here only a set of
but many modifications, for other experiments and observations, were used.
Sure enough, it is trivial to use the HP 48 just to record data (e.g, I used
a lot to collect biometric data on the lizards). 

<h2><a name="why">Why record behavior using an HP48 calculator?</a></h2>
The longer story can be found in
<a href="http://segate.sunet.se/cgi-bin/wa?A2=ind9606&amp;L=ethology&amp;F=&amp;S=&amp;P=4352">
my original summary message</a>
to the Ethology email list, where I summarized the answers I got to my original posting, and the "homework" I did when searching
for a portable and inexpensive behavioral recording device. You will find 
the details, the reasons for the choice (and the alternatives considered) in
the above message but in summary this was the situation:
<ul>
  <li>I was leaving to do field work for at least 6 months, and I wanted a
    way to record lizard behavior that would not require me to then spend
    countless hours transcribing recorded tapes. (I had done that in the
    past, and I hated it). And programming in any reasonable language should
    take just a fraction of transcribing hours of tapes (and would be a lot
    more fun).</li>
  <li>A computer-like device has the advantage of allowing you to program
    pre-specified signals that allow you to execute certain actions at
    certain times, thus making much simpler to follow a pre-scheduled set of
    actions (such as I ended up doing for some of my experiments).</li>
  <li>After examining the alternatives, other options were either extremely
    expensive (e.g., a Psion machine with The Observer) or non-usable (e.g.,
    some TI calculators because they had no clock).</li>
  <li>Thus, I got an HP 48 calculator, and started programming it to fit my
    needs. I actually also fell in love with the calculator and its RPN
    operation, and still keep it closely around.</li>
</ul>

<h2><a name="alternatives">Alternatives: Things I would do differently now</a></h2>
I was very (unpleasantly) surprised to find, after a few Google searches,
that, eight years later, there are not those many alternative options! I
would have expected that with powerful Palms and Pocket PCs things would be
much better, but they aren't. A particularly interesting feature is that new
Pocket PCs and Palms come with a lot more memory than the HP 48 (even the HP
48GX), so the constraints I had to produce non-verbose (and thus, hardly
human editable) output from the HP would be lifted.


<p>There are a few programs
for the Palm but they are both non-free (free in the sense of 
<a href="http://www.gnu.org/philosophy/free-sw.html">free software</a>)
and very expensive. For both philosophical reasons and economical
ones I would not consider these. Things are pretty much the same for the
Pocket PC.</p>


<p>After a quick search in <a href="http://www.google.com">Google</a> I found a
product called "Outdoor explorer", for the Palm, that not only sells for the
very affordable <a
href="http://www.biobserve.com/mobile_systems/outdoor_explorer/prices.html">price</a>
of about 800 &euro; (euro), but is, again, non-free
software. Another non-free program is distributed by
<a href="http://www.pendragon-software.com/">Pendragon software</a> and
sells for about $ 200. A
product from <a href="http://www.skware.com/id27.htm">Educational Consulting</a>for the Windows CE operating system for
Pocket PCs sells for about $ 150 (so on top of being non-free and the price, you
add Windows&hellip;). Sure enough, "The Observer", from Noldus, with a long reputation
in behavioral research, has been ported to Windows CE handhelds. I mention all
of these for the sake of completeness, but I would not consider any of these
programs for my own work; there are
<a href="http://www.gnu.org/philosophy/free-sw.html">philosophical reasons</a>
and many of them, in particular for grad students, carry quite a price tag
(i.e., there are economical reasons). In addition, I don't think most of
those programs would have worked for a situation like mine. Finally,
writing or customizing the code (and customization is only an option with free
or open source code or with code you write yourself) was, for me, an important part of thinking clearly and
throughly about what, how, and why I was trying to measure. </p>



<p>An interesting approach is the one documented by
<a href="http://www.wfu.edu/~mudayja/embed/">Jeff Mudday's embedded systems for
biological research page</a>, also shown in the
<a
href="http://www.wfu.edu/~mudayja/presentations/Ruggedized_Handheld_Computers_in_Avian_Behavioral_Research-2.pdf">handheld
computers presentation</a>. If I were to start, I would surely check all this
more thoroughly. On top of that, I have
heard that programming the Palm is not that hard (there is plenty of
documentation from both the Palm OS site, and several books out there) so
it would be possible to roll your own code, though it might not be as easy as
programming for the HP 48 (which was easy).</p>




<p>An interesting alternative would
be the PocketPC: there are several ports of GNU/Linux, in different stages,
for the PocketPC, and one of them, <a
href="http://familiar.handhelds.org">Familiar</a>,
comes with a full <a
href="http://www.python.org">Python</a>. This would probably be the way to go
for me now. With Python, and without the constraints in size of files, I
could write the programs to record the behavior and then comfortably edit the
output at the end of the    trial. This would also make things a lot easier,
because I could write, run, test, and debug the code on a laptop before
checking it on the handheld. Note, however, that I am not sure that, for
situations such as mine, a Pocket PC or Palm would work well: I made use of a
whole bunch of different keys in the HP 48 when recording behavior. So at
least it would probably be necessary to use an external portable keyboard (I
think there are inexpensive ones, starting at around 20 euro).</p>

<p>Finally, I don't want to end without a mention to
Etholog, a very nice gratis program. I haven't found much about current
development, but if source code were available, it might be possible to make it
run under Windows CE, or even port it to GNU/Linux. My old link to Etholog no
longer seems to work. A quick Google search yields the following link to 
<a
href="http://loadsoft.narod.ru/education_and_science/science_and_engineering/review_52885_index.html">
download etholog.
</a>
</p>


<h2><a name="flow">Basic program flow</a></h2>
<ol>
  <li>The HP 48 programs (exp6, beh6, anq6, cl6) are used, with the HP 48, to
    collect data. (See <a name="BehHP48-manual.html">HP 48 programs
    documentation</a> for details).</li>
  <li>After data from one or more lizards is collected, it is preprocessed to
    get rid of certain symbols, etc. I used an infamous word processor that I
    will not name to do that task. A macro is included at the bottom of
    antipa.cpp. Today, I would probably conduct that task with a <a
    href="http://www.python.org">Python</a> program.</li>
  <li>The preprocessed output is fed to antipa.</li>
  <li>Now, the output from antipa is fixed it, during the behavioral
    recording sequence, you typed the wrong key, or whatever. Essentially,
    what antipa does is put the hard-to-edit output of the HP programs in an
    easy to edit format, that allows correction of mistakes, etc.</li>
  <li>The corrected output is fed to antipb. This produces the basic stuff
    that will then be analyzed (e.g., time hiding, time to full exposure,
    etc, etc).</li>
</ol>

<h2><a name="cmm">The C++ programs</a></h2>

<p>These were written using the Borland IDE. They use some deprecated style, for
example, for inclusion of header files, etc. But they at least compile
without errors (only the warning about the header) under GNU/Linux, using g++
(version 3.3, as of this writing). [Today, I'd probably write this part with
Python instead of C++; at that time, however, I new nothing about Python, and
I wanted to learn C++, so this looked like a good training opportunity.]</p>


<p>The programs that were used for the experiments cited are antipa.cpp and
antipb.cpp (and their corresponding header files). However, I also include
antip20.h, because it defines several classes and methods that would be used to
process the focal data, and obtain frequency of displays and other behaviors.</p>


<h2><a name="hp">The HP 48 programs</a></h2>
They have their own <a href="BehHP48-manual.html">longer explanation</a>.
They were written using a text editor on a computer, and then transferred to
the HP, were they were tested. Probably an easier way to do some of this
today would be to use an HP 48 emulator (there is at least one, I think, for
GNU/Linux). The programs are written in "user RPL", as it used to be called
in the newsgroups, as opposed to "system RPL". User RPL is a relatively
simple lisp-like language, and the information contained in the "Advanced
Users Reference Manual" (you might be able to find pdf versions in the web) is all you need to write programs.

<h2><a name="download">Download</a></h2>

The file <a href="BehHP48.tar.gz">BehHP48.tar.gz</a> is a compressed tar.gz
file that contains the code for the HP 48 programs, the source code for the
C++ files, the documentation, and this file.



<hr />
<address>
  <a href="mailto:rdiaz@ligarto.org">Ramón Díaz-Uriarte</a>
</address>
<!-- Created: Fri Apr 30 08:50:18 CEST 2004 -->
<!-- hhmts start -->Last modified: Tue Jul  6 14:00:35 CEST 2004 <!-- hhmts end -->



<hr />



</div> 




</body>
</html>



