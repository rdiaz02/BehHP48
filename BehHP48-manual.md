<!-- <?xml version="1.0" encoding="iso-8859-15"?> -->
<!-- <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"> -->
<!-- <html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en"> -->
<!-- <head> -->
<!-- <meta name="generator" content="XEmacs http://www.xemacs.org" /> -->
<!-- <meta name="author" content="Ram&oacute;n D&iacute;az-Uriarte" /> -->
<!-- <meta name="keywords" content="behavior animal recording HP48 RPL programm" /> -->
<!-- <meta name="description" content="Documentation for BehHP48: a set of HP 48 -->
<!-- calculator programs for recording behavior" /> -->
<!-- <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-15" /> -->
<!-- <link rel="stylesheet" type="text/css" href="../RDUstyle1.css" /> -->
<!-- <title>Documentation for the BehHP48 Programs</title> -->
<!-- </head> -->

<!-- <body> -->
<!-- <div id="page"> -->



<!-- <div id="sectionnav"> -->
<!-- <p><span class="sidetitle">Document contents</span></p> -->
<!--   <a href="#Set">The set of programs</a> -->
<!-- <a href="#bundle">Structure and use of the bundle</a> -->
<!--   <a href="#What">What the HP 48 programs do</a> -->
<!--   <a href="#Cmm">The C++ programs</a> -->
<!-- <a href="#How">How the programs work: details</a> -->
<!-- <a href="#alarms">Some details of how alarms and counter work in the antipredator part</a> -->
<!-- <a href="#focal">Duration of focal session</a> -->
<!-- <a href="#new">New stuff for the exp programs</a> -->
<!-- <a href="#stand">Standardizing times</a> -->
<!-- <a href="#flow">General comments on flow of program</a> -->
<!-- <a href="#fazenda">Comments on a program version for the experiment in Fazenda Santo Antonio</a> -->
<!-- <a href="#encl">Enclosures version (the one available)</a> -->
<!-- <a href="#SEC1">GNU Free Documentation License</a> -->
<!-- <a href="#SEC4">How to use this License for your documents</a>   -->
 
<!-- </div> <\!-- sectionnav -\-> -->



<h1>Documentation for BehHP48: a set of HP 48 Calculator Programs for Recording Behavior</h1>


<br />
<hr />
<pre>
      Copyright (c)  1996, 2004 Ram&oacute;n D&iacute;az-Uriarte.
      Permission is granted to copy, distribute and/or modify this document
      under the terms of the GNU Free Documentation License, Version 1.2
      or any later version published by the Free Software Foundation;
      with no Invariant Sections, no Front-Cover Texts, and no Back-Cover
      Texts.  A copy of the license is included in the section entitled
      "GNU Free Documentation License".
</pre>



<hr />

<h2><a name="Set">The set of programs</a></h2>

  The <strong>BehHP48</strong> program bundle
consists of three main subroutines: beh6, anq6, and exp6 (CL is
  a utility program that tells you the time,date, and memory available, and
  deletes unnecessary junk --that is created if you exit the program
abnormally). In addition, two C++ programs (antipa and antipb) produce
human-editable output for checking and fixing (antipa) and return the
behavioral data, such as time to hide, time hiding, etc (antipb).

<h2><a name="bundle">Structure and use of the bundle</a></h2>
<ol>
  <li>The HP 48 programs (exp6, beh6, anq6, cl6) are used, with the HP 48, to
    collect data. </li>
  <li>After data from one or more lizards is collected, it is preprocessed to
    get rid of certain symbols, etc. I used an infamous word processor that I
    will not name to do that task. A macro is included at the bottom of
    antipa.cpp. Today, I would no doubt conduct that task with a <a
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



<h2><a name="What">What the HP 48 programs do</a></h2>
  Basically: at the start of the run (which is controlled by beh6) you are
  asked a few initial questions (lizard ID, enclosure number, etc). There is
  code that will allow to enter focal data, but that is commented now. Then,
  the whole set of actions starts, and the program produces beeps and messages
  at prespecified times, to let you know what to do (e.g., introduce intruder,
  etc).  Then, at the right time and sequence of events, the beh6 program is
  started, and run from within exp6. beh6 contains the set of key combinations
  (and noises) for the behaviors. Finally, at a prespecified time the anq6
  program is launched, which is used to collect some extra information at the
  end of the run.




<!-- 	Originally, the programs consisted of more units, which are now -->
<!-- 	integrated into the main programs.  This reduces "modularity", but also -->
<!-- 	reduces the clutter in the directories, by having just two important -->
<!-- 	programs. ompared to previous programs and versions: -Al1 is now a -->
<!-- 	local variable defined in beh3.  -All1 (and all2, etc) is now extended -->
<!-- 	as text in beh3. -->



<h2><a name="Cmm">The C++ programs</a></h2>
These were written using the Borland IDE. They use some deprecated style, for
example, for inclusion of header files, etc. But they at least compile
without errors (only the warning about the header) under GNU/Linux, using g++
(version 3.3, as of this writing). [Today, I'd probably write this part with
<a href="http://www.python.org">Python</a> instead of C++; at that time, however, I new nothing about Python, and
I wanted to learn C++, so this looked like a good training opportunity.]


<p>The programs that were used for the experiments cited are antipa.cpp and
antipb.cpp (and their corresponding header files). However, I also include
antip20.h, because it defines several classes and methods that would be used to
process the focal data, and obtain frequency of displays and other behaviors.</p>

<p>The C++ programs will not be commented any further in these notes.</p>


<h2><a name="How">How the programs work: details</a></h2>

<p>[For information on the workings of alarms see below].</p>

<p>exp6 is the master program.  It first initializes flags, clears junk,
	etc.  Then, it asks several questions.  And, right before calling the
	beh6 program for the focal part, it initializes Ts and Te, which are
	used to keep track of the duration of the focal session (see below:
	Duration of focal session).  When you start the program (and if flags
	are in the proper state) you always enter this module.</p>

<p>beh6 has been called; it is operating as the focal program.  When the
	predetermined duration of the focal is due, an alarm sounds.  Then, you
	press the 65.3 (left arrow and division) to signal the end of the focal
	session.  This sets flag 3.  Flag 3, plus flag 7 (which was set when
	you started exp1) make the beh6 program behav appropriately for this
	second part: when you press 0 you will see "My move", you will not mess
	with the counter of antipred moves, and, when the animal moves or is
	lost, the appropriate alarm is set.  As you see, the approach part is
	really another set of cycles over the while loop in beh6, without
	exiting it; we did this by not changing the value of flag 2; as flag 2
	is still set, in between the focal and the approach part, the while
	loop is still working.  But, after the animal moves or is lost in the
	approach phase, if you press the 65.3 you will exit the loop.  After
	exiting the loop, beh6 calls exp1 again, but now with a different value
	for flag 8.</p>

<p>Again in exp6.  If things go well, after the appropriate time for the
	"approach phase", the lizard will be out again.  Therefore, when you are
	asked whether to run the antipredator or not, just press anything and
	enter (anything except NO!).  Then, you will start the antipredator
	program, which works just as usual.  When the beh6 was to be run for
	the antipredator part flag 9 was changed; now, when you exit the beh6
	program, you will again call the exp1 program, and with the new value
	for flag 9, you call the anq6 program, which contains the antipredator
	questions.  If you never entered the beh6 for the antipredator part, you
	called the anq6 program.  anq6 asks you only the questions of the
	approach part if you never run the post-treatment antipredator test; it
	asks you all the questions if you run it.</p>

<p>(Note: beh6 is
exited sometimes in the middle, sometimes in the end; this is because the
alarms interrupt the program, and everything is left on the stack; that is why
alarms, when due, not only produce a lovely music, but also call some program
to start execution.)</p>

<p>Flag 8: it is not really necessary to clear flag 8 after animal lost or
	no access in antipred part.  Because, as flag 9 is set right before the
	antipred part starts, the program , in next run, will run the anq6
	part.  It IS necessary that flag 8 is set in the approach 1 part (so
	that we start the antipred part, in the exp1).  I leave the clearing of
	flag8: it is a reminiscence of the old caico programs, and could be
	used in the new ones.</p>



<h2><a name="alarms">Some details of how alarms and counter work in the antipredator part</a></h2>

(Some of these are slightly obsolete)
In the antipredator trial, I use alarms (as usual with my antipredator
programs).  These alarms interrupt the flow of the program, leaving everything
in the stack.  I copy from the documentation of Behav4.sub:

<p>@Most of the following comments that refer to alarms are just for the
antipredator part; none of these alarms should be set with the focal program
(because you should not press "my move", or "no access" , or the special
"lizard lost" --different from "lost"; "lost" just means the lizard hides;
"lizard lost" is ONLY when carrying out the antipredator test; is the first
time the lizard is lost, as a consequence of my approach@</p>

<p>@Alarms: one alarm beeps so that I make my next move (15") after stopping
(remember that I stop right after the first movement of the lizard after my
starting to move); the second alarm beeps to end the session (7' after lizard
hides).  These are control alarms, and they are regulated by ALL2 and AL2. ALL2
sets the timing of the alarm (15" or 7', depending on the state of flag 4); the
alarm executes AL2, which contains a set of beeps, and a call to
BEHAV4.SUB. (i.e., to this very subroutine).  With control alarms the flow of
the program is interrupted when the alarm is due, and you are returned to the
stack.  Therefore, it is necessary to call BEHAV4.SUB again. The program clears
system flag -44, so that the acknowledged alarms are not saved in the system
alarm list. @</p>


<p>@The flow and flag setting can seem confusing, but they allow to
correct a nasty mistake: if you get obfuscated and press Z --lost-- when the
lizard is not really hiding, nothing irreparable happens; you just have to
press 0 when it is time to move again, move, and continue as usual.  This way,
the right number of movements will be recorded@</p>

<p>@ Counter and alarm will be set
only if the lizard moves after I have approached; if I am already stopped, but
the lizard makes further movements, this should not increase the counter (or
sets the alarm).  When I move, I set flag 4; this flag is on until the lizard
first moves --then, it clears flag 4--; if the lizard moves or suddenly hides,
and flag 4 is set, then the counter counts; the alarm is set if there is
movement.  The alarm is cleared when the lizard hides or I get to "no access";
in these cases, the 7' alarm is set.  If the lizard starts moving and then
disappears, the counter only increases once, as it should be: with movement,
flag 4 is cleared, and in "lost lizard" the counter is not increased@</p>


<p>New changes  (that do affect beh6, etc):</p>
<ul>
<li> all1, all2, etc, are no longer used.  All2 is "expanded in
line"; all2 (actually called all1 now) is defined as a local variable at the
beginning of the program.  </li>
<li> I have rechecked the program, and there have been
some minor changes.  </li>
<li> I have tried to add more protection against other
possible mistakes, but the program is not full-proof, of course.   Here are some
  comments:
<ul>
  
  <li>If you press "Lizard lost" (Z) twice, it is only the last one that
  counts, in terms of alarms.  This is what is of most help when using the
  program.  If you make a mistake and press Z, you can "correct" it, and then, at
  the end, when you press the last "Z", this is the one which counts.  This is
  DIFFERENT from what happens with "No access"; here, is the first one which
  counts; again, this is likely to be the most helpful implementation.  In
  contrast to what happens with Z, it is unlikely that you will press SPC unless
  the animal is really SPC.</li>
  
  <li>One nasty mistake: suppose you have the sequence: 0...SPC.T.0....Z;
  here, you made a mistake, and pressed SPC, but it was not right.  The
  calculator will tell there was only 1 run; and this is the only thing
  that makes sense, because it MUST interpret the T as a T done after
  either a SPC or a lost, and those T no longer increase the counter.
  This is the only way to handle appropriately the normal, correct,
  sequence of data entrance.  If that happens, a solution is to key:
  0...SPC.0.T.0...Z; here, you'll get the right number of moves, if SPC
  was a mistake.</li>
  
  <li>Flag 10 allows to distinguish between the antipredator and the approach
  1 runs.  In approach 1, if the lizard moves, its first movement, sets
  the alarm, and further movements wont.  It is the same for lizard lost:
  if you press lizard lost, only the first sets the alarm. If you press
  move and then lost, only move works, and if you press lost and then
  move, the alarm was set by lost. The idea is that: a) you can press
  move after the lizard has reemerged, so it is not reasonable to give
  any move the ability to set alarms; b) with lizard-lost the problem is
  that, if you allow it to set alarms after movement, animals that tend
  to get lost a while after moving will have their alarms set later than
  animals that just move; this could introduce perverse biases, etc.  So
  here, in opposition to the safeguard in the antipredator part, you
  better not make mistakes when pressing lizard lost (if that is the
  first thing after I move).</li>
</ul>
</li>
</ul>




<h2><a name="focal">Duration of focal session</a></h2>

The calculator keeps track of the net time of observation of the animal (i.e,
it discounts the time the animals is lost).  An alarm will sound when the net
time is the same as the duration you want for the focal session. Here is how it
works:

<p>When it starts the value of TS (time starts) and TE (time elapsed) are
initialized as 0 (the format is HP binary integer because these are later added
to the TICKS from the HP: therefore the # 0d). When beh6 stars, the value of TS
is taken from TICKS, and the alarm is set for 15' (see below for alarms). If
the animal is lost, the alarms are deleted, and time elapsed is calculated as
time elapsed + (hour when it is lost --obtained from TICKS-- minus starting
hour --TS--).  If the animal is found, the alarm is set for a time equal to 15'
minus the time elapsed, and the current TICKS becomes TS.</p>

<p>(Even if you make a mistake and press found when it shouldn't nothing bad
happens: all alarms are deleted at exit of the program, and all are deleted at
Lost; therefore, the first alarm you will hear is the one corresponding to the
first found after the animal was lost.  If you press lost twice, only the first
one after a found is valid --flag 6 takes care of this).</p>

<p>Alarms: to the time for the alarm in ticks (8192 * 60 *15) you subtract the TE
(after making it a real); this is divided by 29491200 (the number of ticks in
an hour), to get the time for the alarm as fractions of hour (decimal
representation); this number is converted into a regular HH.MMSSsss number, and
added to the current time, to set the hour of the alarm.</p>

<h2><a name="new">New stuff for the exp programs</a></h2>

There have been many additional changes. Main changes:

<h3>Flags</h3>

<p>In the previous version, the use of flags was a bit confusing and there were
redundancies; now, it is still confusing, but not so much. Before, flags
3,7,8,9, and 10 were partially redundant.  These are no longer used.  Now,
flags are as follows:</p>

<ul>
  <li>2:Controls the while loop in bheav.  Never touch it.</li>
<li>4:Controls alarms in
antipredator part.</li>
<li>5:Controls no access in antipredator.</li>
<li>6:Controls alarms
for the duration of focal session, in the "focal" part.</li>
</ul>

<p>These flags did the same thing in the previous version, and have not been
changed. </p>


<p>New flags are:</p>

<ul>
  <li>Flags 20,21, and 22:  control whether we are in:
<br />
<!-- <table cellpadding="1" summary="State of flags 20, 21, 22" cellspacing="1" border="1" align="center"> -->
  <table cellpadding="1" summary="State of flags 20, 21, 22" cellspacing="1" border="1">
	<tr><td>            </td><td>Flag 20 </td><td>Flag 21</td><td>Flag 22</td></tr>
	<tr><td>Focal       </td><td>clear   </td><td>clear  </td><td>clear</td></tr>
	<tr><td>Approach 1  </td><td>clear   </td><td>clear  </td><td>set </td></tr>
	<tr><td>Antipredator</td><td>set     </td><td>clear  </td><td>clear</td></tr>
	<tr><td>Anq4        </td><td>doesn't matter</td><td>set</td><td>doesn't matter</td></tr>
</table>
<br />
These flags modify program flow both in exp12 and in beh4.

</li>

<li> Flag 30: if set, the treatment is control, otherwise it is an intruder (this
flag will control, in beh4, the working of some alarms).</li>

<li>Flag 31: if clear, it means there is still no attack, bite, or poke; if clear,
at least one of either of those behaviors already happened.  This is to know
when the alarm for those should be set (in the first one).  If the flag is set,
the alarm for those behaviors will not be set again; it is only set when the
first one takes place.</li>

<li>Flag 32: if set, animal is lost.</li>

<li>System flags 43 and 44 are used to control what the calculator does with alarms
and alarm indexes.  They allow for nicer output, etc.</li>

</ul>



<h2><a name="stand">Standardizing times</a></h2>

<p>When the treatment is control, and if the animal is NOT hiding, we wait a
specified time (TCONTR) to give the antipredator test.  TCONTR is variable, and
is equal to the time that was waited between leaving the intruder (or control)
and giving the antipr test in the last previous test. If the animal hides when
I place the intruder, then TCONR is equal to the time between the animal
reemerges and the antipredator test is given.  [Actually, time is calculated as
time between pressing 2 (83.1) and the time the final alarm was due in the
previous (successful) test; either it there was an intruder, who was attacked,
or there was a control; not if the previous was a case where the focal did not
reemerge.  Note that this is the time we want; when the alarm sounds, we then
will proceed to the antipr. test; this is what makes most similar the real time
between 2 and antipr in the control and the previous trial].</p>

<p> It is not possible to completely standardize times.  There are other options,
 which are probably worse:</p>
<ul>

<li>We could set a constant time after something like
 "lizard pays attention"; but this is a very subjective assessment, and I will
 tend to make this shorter in the control than in the intruder case: for the
 intruder, I will judge the lizard to have payed attention when it looks at the
 intruder and does some high intensity displays. I do not expect the intruder
 to do displays to the control, so as soon as it looks at the control, I will
 tend to consider it has "payed attention".  Also, with this method I will tend
 to make some time intervals (till antipred) longer than they need to be.</li>

<li> We could set a constant time after I leave the control or intruder.  But
animals that hide will have shorter times between attack to intruder and
antipredator than animals that don't hide. So, animals that are more shy have,
systematically, sorter times till antipredator.  This is a very dangerous
systematic bias.</li>

<li> We could set a constant time after attack; this seems the best.  But there
are some details: a) What about controls?  Controls will not be attacked, so
the best I can do is leave the stimulus there for some time, more or less
similar to the time the stimulus is left there when the intruder is alive. (so
focal is exposed to control, when focal is NOT hiding, for similar time as if
it were an intruder, when NOT hiding) b) What if attack is not over?  I cannot
wait forever, so I set a maximum time for the antipredator, after the attack is
initiated; this I have set to 10 minutes; c) What if no attack: I wait a
maximum of 8 minutes and 30 seconds for an attack to take place.  But, if
everything goes well, the main alarm will be the one that is set for 5' after
the attack stops; I consider an attack to be over when the focal is no longer
running after the intruder for at least 15".</li>
</ul>


<h2><a name="flow">General comments on flow of programs for HP</a></h2>

<p>Here are some comments on how the program works for the approach 1 part (the
others are documented above); some other things can be found on the comments in
the code itself.</p>
<ul>
<li> If an animal is lost, I set up alarm ALR for time equal to treap, and set
flag 32.</li>

<li> If an animal reappears (i.e, does likely stuff after reappearing, such as
move, bobs, Gbobs, or keying found), then, as flag 32 should be set, I delete
all alarms, set the alarm for the 15" scans, and set the corresponding alarm
either for control (with TCONTR) or for maximum time till attack (ALAT, with
tatck, and set flag 31).  Alarm 32 is cleared.</li>

<li> An animal could reemerge doing an attack, bite or poke as the first thing; in
such case, I set alarms for scans and AL1 for taas --maximum time an attack can
last before giving an antipred-- (flag 31 is cleared).</li>

<li> When an attack, bite or poke takes place (not first thing after being lost),
the "2 delalarm" is used to get rid of the "maximum time till attack" alarm
(ALAT); also, flag 31 is cleared, so this will not be done again in successive
bites, attacks, or pokes. And AL1 for taas is set.  So this case and the above
are very similar.</li>

<li> When an attack ends, AL1 is set for 5'.  BUT: note that if the attack started
at minute 1, and ended at minute 7, the alrm will be set for minute 12.  But
before this alarm works, the alarms for taas (10 minutes) will be activated;
this is to prevent a very long sequence due to a very long attack, that ends
and then is followed by the 5'; this way, the maximum time between an attack
and the antipr is 10', regardless of whether the attack ends or not.</li>

<li> The work of TCONTR is simple: a first time (TIP2: time I place 2) is recorded
when I am back, or when the focal reappears if it hide; and this is subtracted
from the time AL1 is activated [there is a subtraction of 1.2 seconds, because
of a lag (due to the beeps, etc).]</li>

<li> The alarms for the scans only present when the animal is not hiding.</li>

<li> If there is an attack in control (well,maybe the can is very
aggression-provoking, or the animal went crazy, or a real intruder shows up),
things will work as if there was an intruder.</li>

</ul>



<h2><a name="fazenda">Comments on a program version for the experiment in Fazenda Santo Antonio</a></h2>

<ol>
<li> The programs are exp15, cl5, beh5, anq5.  They are very similar to the ones
with # 4. </li>

<li> In anq5, there are changes in the questions asked; basically, there are no
questions about location (of course, because I have no maps), and many other
questions have been deleted: I need to be very fast, and avoid making useless
questions.</li>

<li> Now I fix the duration of the attack: 3 minutes; then I take the intruder
back, wait another 3', and give the antipredator test.</li>

<li> I wait a maximum of 15' till an animal attacks.</li>

<li> If control, the time between I leave the can and give the antipredator is
equal to the time, in the previous intruder, between I left the can and gave
the antipred. test.</li>


<li> ALA: it is the alarm set when first attack/bite/poke; computes Tcontr;
time is datck.  AL1: used in  appr, after I press 2; time is taae.  ALR: if animal
does not attack in tatck.  ALC: alarm end control.</li>

<li> Flag 30: if set, it is a control, if clear it is an intruder;</li>

<li>Flag 31: if clear still no
attack or bite or poke; set: some.</li>

<li> taat: duration of attack; now datck; taas: time after attack ends: now taae;
treap: eliminated.</li>

<li> When I leave the animal I press 1, when I recover it I press 2; at the end of
  recovery, when pressing, taae is set.</li>
</ol>
  
<h2><a name="encl">Enclosures version (the one available)</a></h2>

Follows the stuff for Fazenda, but some differences: TCONTR is not used
now, and so ALA is not used.  When I start to move the intruder, I press 0; 
  when the intruder is back, I press 1;  when it starts to come out I press
  ".";  and when it is all back, I p ress 2. After that, we wait 2 minutes.
There are a few other changes in the antipredator questions; they are
  documented in the program itself.



<hr />
<hr />

<h2><a name="SEC1">GNU Free Documentation License</a></h2>
<p>Version 1.2, November 2002 </p>

<pre>
Copyright (C) 2000,2001,2002  Free Software Foundation, Inc.
59 Temple Place, Suite 330, Boston, MA  02111-1307  USA
Everyone is permitted to copy and distribute verbatim copies
of this license document, but changing it is not allowed.
</pre>


<p>
<strong>0. PREAMBLE</strong>
</p><p>
The purpose of this License is to make a manual, textbook, or other
functional and useful document "free" in the sense of freedom: to
assure everyone the effective freedom to copy and redistribute it,
with or without modifying it, either commercially or noncommercially.
Secondarily, this License preserves for the author and publisher a way
to get credit for their work, while not being considered responsible
for modifications made by others.
</p><p>
This License is a kind of "copyleft", which means that derivative
works of the document must themselves be free in the same sense.  It
complements the GNU General Public License, which is a copyleft
license designed for free software.
</p><p>
We have designed this License in order to use it for manuals for free
software, because free software needs free documentation: a free
program should come with manuals providing the same freedoms that the
software does.  But this License is not limited to software manuals;
it can be used for any textual work, regardless of subject matter or
whether it is published as a printed book.  We recommend this License
principally for works whose purpose is instruction or reference.
</p><p>

<strong>1. APPLICABILITY AND DEFINITIONS</strong>
</p><p>
This License applies to any manual or other work, in any medium, that
contains a notice placed by the copyright holder saying it can be
distributed under the terms of this License.  Such a notice grants a
world-wide, royalty-free license, unlimited in duration, to use that
work under the conditions stated herein.  The "Document", below,
refers to any such manual or work.  Any member of the public is a
licensee, and is addressed as "you".  You accept the license if you
copy, modify or distribute the work in a way requiring permission
under copyright law.
</p><p>
A "Modified Version" of the Document means any work containing the
Document or a portion of it, either copied verbatim, or with
modifications and/or translated into another language.
</p><p>
A "Secondary Section" is a named appendix or a front-matter section of
the Document that deals exclusively with the relationship of the
publishers or authors of the Document to the Document's overall subject
(or to related matters) and contains nothing that could fall directly
within that overall subject.  (Thus, if the Document is in part a
textbook of mathematics, a Secondary Section may not explain any
mathematics.)  The relationship could be a matter of historical
connection with the subject or with related matters, or of legal,
commercial, philosophical, ethical or political position regarding
them.
</p><p>
The "Invariant Sections" are certain Secondary Sections whose titles
are designated, as being those of Invariant Sections, in the notice
that says that the Document is released under this License.  If a
section does not fit the above definition of Secondary then it is not
allowed to be designated as Invariant.  The Document may contain zero
Invariant Sections.  If the Document does not identify any Invariant
Sections then there are none.
</p><p>
The "Cover Texts" are certain short passages of text that are listed,
as Front-Cover Texts or Back-Cover Texts, in the notice that says that
the Document is released under this License.  A Front-Cover Text may
be at most 5 words, and a Back-Cover Text may be at most 25 words.
</p><p>
A "Transparent" copy of the Document means a machine-readable copy,
represented in a format whose specification is available to the
general public, that is suitable for revising the document
straightforwardly with generic text editors or (for images composed of
pixels) generic paint programs or (for drawings) some widely available
drawing editor, and that is suitable for input to text formatters or
for automatic translation to a variety of formats suitable for input
to text formatters.  A copy made in an otherwise Transparent file
format whose markup, or absence of markup, has been arranged to thwart
or discourage subsequent modification by readers is not Transparent.
An image format is not Transparent if used for any substantial amount
of text.  A copy that is not "Transparent" is called "Opaque".
</p><p>
Examples of suitable formats for Transparent copies include plain
ASCII without markup, Texinfo input format, LaTeX input format, SGML
or XML using a publicly available DTD, and standard-conforming simple
HTML, PostScript or PDF designed for human modification.  Examples of
transparent image formats include PNG, XCF and JPG.  Opaque formats
include proprietary formats that can be read and edited only by
proprietary word processors, SGML or XML for which the DTD and/or
processing tools are not generally available, and the
machine-generated HTML, PostScript or PDF produced by some word
processors for output purposes only.
</p><p>
The "Title Page" means, for a printed book, the title page itself,
plus such following pages as are needed to hold, legibly, the material
this License requires to appear in the title page.  For works in
formats which do not have any title page as such, "Title Page" means
the text near the most prominent appearance of the work's title,
preceding the beginning of the body of the text.</p>
<p>
A section "Entitled XYZ" means a named subunit of the Document whose
title either is precisely XYZ or contains XYZ in parentheses following
text that translates XYZ in another language.  (Here XYZ stands for a
specific section name mentioned below, such as "Acknowledgements",
"Dedications", "Endorsements", or "History".)  To "Preserve the Title"
of such a section when you modify the Document means that it remains a
section "Entitled XYZ" according to this definition.</p>
<p>
The Document may include Warranty Disclaimers next to the notice which
states that this License applies to the Document.  These Warranty
Disclaimers are considered to be included by reference in this
License, but only as regards disclaiming warranties: any other
implication that these Warranty Disclaimers may have is void and has
no effect on the meaning of this License.
</p><p>
<strong>2. VERBATIM COPYING</strong>
</p><p>
You may copy and distribute the Document in any medium, either
commercially or noncommercially, provided that this License, the
copyright notices, and the license notice saying this License applies
to the Document are reproduced in all copies, and that you add no other
conditions whatsoever to those of this License.  You may not use
technical measures to obstruct or control the reading or further
copying of the copies you make or distribute.  However, you may accept
compensation in exchange for copies.  If you distribute a large enough
number of copies you must also follow the conditions in section 3.
</p><p>
You may also lend copies, under the same conditions stated above, and
you may publicly display copies.
</p><p>

<strong>3. COPYING IN QUANTITY</strong>
</p><p>
If you publish printed copies (or copies in media that commonly have
printed covers) of the Document, numbering more than 100, and the
Document's license notice requires Cover Texts, you must enclose the
copies in covers that carry, clearly and legibly, all these Cover
Texts: Front-Cover Texts on the front cover, and Back-Cover Texts on
the back cover.  Both covers must also clearly and legibly identify
you as the publisher of these copies.  The front cover must present
the full title with all words of the title equally prominent and
visible.  You may add other material on the covers in addition.
Copying with changes limited to the covers, as long as they preserve
the title of the Document and satisfy these conditions, can be treated
as verbatim copying in other respects.
</p><p>
If the required texts for either cover are too voluminous to fit
legibly, you should put the first ones listed (as many as fit
reasonably) on the actual cover, and continue the rest onto adjacent
pages.
</p><p>
If you publish or distribute Opaque copies of the Document numbering
more than 100, you must either include a machine-readable Transparent
copy along with each Opaque copy, or state in or with each Opaque copy
a computer-network location from which the general network-using
public has access to download using public-standard network protocols
a complete Transparent copy of the Document, free of added material.
If you use the latter option, you must take reasonably prudent steps,
when you begin distribution of Opaque copies in quantity, to ensure
that this Transparent copy will remain thus accessible at the stated
location until at least one year after the last time you distribute an
Opaque copy (directly or through your agents or retailers) of that
edition to the public.
</p><p>
It is requested, but not required, that you contact the authors of the
Document well before redistributing any large number of copies, to give
them a chance to provide you with an updated version of the Document.
</p><p>

<strong>4. MODIFICATIONS</strong>
</p><p>
You may copy and distribute a Modified Version of the Document under
the conditions of sections 2 and 3 above, provided that you release
the Modified Version under precisely this License, with the Modified
Version filling the role of the Document, thus licensing distribution
and modification of the Modified Version to whoever possesses a copy
of it.  In addition, you must do these things in the Modified Version:</p>

<ul>
<li><strong>A.</strong> Use in the Title Page (and on the covers, if any) a title distinct
   from that of the Document, and from those of previous versions
   (which should, if there were any, be listed in the History section
   of the Document).  You may use the same title as a previous version
   if the original publisher of that version gives permission.
</li><li><strong>B.</strong> List on the Title Page, as authors, one or more persons or entities
   responsible for authorship of the modifications in the Modified
   Version, together with at least five of the principal authors of the
   Document (all of its principal authors, if it has fewer than five),
   unless they release you from this requirement.
</li><li><strong>C.</strong> State on the Title page the name of the publisher of the
   Modified Version, as the publisher.
</li><li><strong>D.</strong> Preserve all the copyright notices of the Document.
</li><li><strong>E.</strong> Add an appropriate copyright notice for your modifications
   adjacent to the other copyright notices.
</li><li><strong>F.</strong> Include, immediately after the copyright notices, a license notice
   giving the public permission to use the Modified Version under the
   terms of this License, in the form shown in the Addendum below.
</li><li><strong>G.</strong> Preserve in that license notice the full lists of Invariant Sections
   and required Cover Texts given in the Document's license notice.
</li><li><strong>H.</strong> Include an unaltered copy of this License.
</li><li><strong>I.</strong> Preserve the section Entitled "History", Preserve its Title, and add
   to it an item stating at least the title, year, new authors, and
   publisher of the Modified Version as given on the Title Page.  If
   there is no section Entitled "History" in the Document, create one
   stating the title, year, authors, and publisher of the Document as
   given on its Title Page, then add an item describing the Modified
   Version as stated in the previous sentence.
</li><li><strong>J.</strong> Preserve the network location, if any, given in the Document for
   public access to a Transparent copy of the Document, and likewise
   the network locations given in the Document for previous versions
   it was based on.  These may be placed in the "History" section.
   You may omit a network location for a work that was published at
   least four years before the Document itself, or if the original
   publisher of the version it refers to gives permission.
</li><li><strong>K.</strong> For any section Entitled "Acknowledgements" or "Dedications",
   Preserve the Title of the section, and preserve in the section all
   the substance and tone of each of the contributor acknowledgements
   and/or dedications given therein.
</li><li><strong>L.</strong> Preserve all the Invariant Sections of the Document,
   unaltered in their text and in their titles.  Section numbers
   or the equivalent are not considered part of the section titles.
</li><li><strong>M.</strong> Delete any section Entitled "Endorsements".  Such a section
   may not be included in the Modified Version.
</li><li><strong>N.</strong> Do not retitle any existing section to be Entitled "Endorsements"
   or to conflict in title with any Invariant Section.
</li><li><strong>O.</strong> Preserve any Warranty Disclaimers.</li>
</ul>
<p>
If the Modified Version includes new front-matter sections or
appendices that qualify as Secondary Sections and contain no material
copied from the Document, you may at your option designate some or all
of these sections as invariant.  To do this, add their titles to the
list of Invariant Sections in the Modified Version's license notice.
These titles must be distinct from any other section titles.
</p><p>
You may add a section Entitled "Endorsements", provided it contains
nothing but endorsements of your Modified Version by various
parties--for example, statements of peer review or that the text has
been approved by an organization as the authoritative definition of a
standard.
</p><p>
You may add a passage of up to five words as a Front-Cover Text, and a
passage of up to 25 words as a Back-Cover Text, to the end of the list
of Cover Texts in the Modified Version.  Only one passage of
Front-Cover Text and one of Back-Cover Text may be added by (or
through arrangements made by) any one entity.  If the Document already
includes a cover text for the same cover, previously added by you or
by arrangement made by the same entity you are acting on behalf of,
you may not add another; but you may replace the old one, on explicit
permission from the previous publisher that added the old one.
</p><p>
The author(s) and publisher(s) of the Document do not by this License
give permission to use their names for publicity for or to assert or
imply endorsement of any Modified Version.
</p><p>

<strong>5. COMBINING DOCUMENTS</strong>
</p><p>
You may combine the Document with other documents released under this
License, under the terms defined in section 4 above for modified
versions, provided that you include in the combination all of the
Invariant Sections of all of the original documents, unmodified, and
list them all as Invariant Sections of your combined work in its
license notice, and that you preserve all their Warranty Disclaimers.
</p><p>
The combined work need only contain one copy of this License, and
multiple identical Invariant Sections may be replaced with a single
copy.  If there are multiple Invariant Sections with the same name but
different contents, make the title of each such section unique by
adding at the end of it, in parentheses, the name of the original
author or publisher of that section if known, or else a unique number.
Make the same adjustment to the section titles in the list of
Invariant Sections in the license notice of the combined work.
</p><p>
In the combination, you must combine any sections Entitled "History"
in the various original documents, forming one section Entitled
"History"; likewise combine any sections Entitled "Acknowledgements",
and any sections Entitled "Dedications".  You must delete all sections
Entitled "Endorsements."
</p><p>

<strong>6. COLLECTIONS OF DOCUMENTS</strong>
</p><p>
You may make a collection consisting of the Document and other documents
released under this License, and replace the individual copies of this
License in the various documents with a single copy that is included in
the collection, provided that you follow the rules of this License for
verbatim copying of each of the documents in all other respects.
</p><p>
You may extract a single document from such a collection, and distribute
it individually under this License, provided you insert a copy of this
License into the extracted document, and follow this License in all
other respects regarding verbatim copying of that document.
</p><p>


<strong>7. AGGREGATION WITH INDEPENDENT WORKS</strong>
</p><p>
A compilation of the Document or its derivatives with other separate
and independent documents or works, in or on a volume of a storage or
distribution medium, is called an "aggregate" if the copyright
resulting from the compilation is not used to limit the legal rights
of the compilation's users beyond what the individual works permit.
When the Document is included in an aggregate, this License does not
apply to the other works in the aggregate which are not themselves
derivative works of the Document.
</p><p>
If the Cover Text requirement of section 3 is applicable to these
copies of the Document, then if the Document is less than one half of
the entire aggregate, the Document's Cover Texts may be placed on
covers that bracket the Document within the aggregate, or the
electronic equivalent of covers if the Document is in electronic form.
Otherwise they must appear on printed covers that bracket the whole
aggregate.
</p><p>

<strong>8. TRANSLATION</strong>
</p><p>
Translation is considered a kind of modification, so you may
distribute translations of the Document under the terms of section 4.
Replacing Invariant Sections with translations requires special
permission from their copyright holders, but you may include
translations of some or all Invariant Sections in addition to the
original versions of these Invariant Sections.  You may include a
translation of this License, and all the license notices in the
Document, and any Warranty Disclaimers, provided that you also include
the original English version of this License and the original versions
of those notices and disclaimers.  In case of a disagreement between
the translation and the original version of this License or a notice
or disclaimer, the original version will prevail.</p>
<p>
If a section in the Document is Entitled "Acknowledgements",
"Dedications", or "History", the requirement (section 4) to Preserve
its Title (section 1) will typically require changing the actual
title.
</p><p>

<strong>9. TERMINATION</strong>
</p><p>
You may not copy, modify, sublicense, or distribute the Document except
as expressly provided for under this License.  Any other attempt to
copy, modify, sublicense or distribute the Document is void, and will
automatically terminate your rights under this License.  However,
parties who have received copies, or rights, from you under this
License will not have their licenses terminated so long as such
parties remain in full compliance.
</p><p>

<strong>10. FUTURE REVISIONS OF THIS LICENSE</strong>
</p><p>
The Free Software Foundation may publish new, revised versions
of the GNU Free Documentation License from time to time.  Such new
versions will be similar in spirit to the present version, but may
differ in detail to address new problems or concerns.  See
<a href="http://www.gnu.org/copyleft/">http://www.gnu.org/copyleft/</a>.
</p>
<p>Each version of the License is given a distinguishing version number.
If the Document specifies that a particular numbered version of this
License "or any later version" applies to it, you have the option of
following the terms and conditions either of that specified version or
of any later version that has been published (not as a draft) by the
Free Software Foundation.  If the Document does not specify a version
number of this License, you may choose any version ever published (not
as a draft) by the Free Software Foundation.</p>

<h2><a name="SEC4">How to use this License for your documents</a></h2>

To use this License in a document you have written, include a copy of
the License in the document and put the following copyright and
license notices just after the title page:



<pre>
      Copyright (c)  YEAR  YOUR NAME.
      Permission is granted to copy, distribute and/or modify this document
      under the terms of the GNU Free Documentation License, Version 1.2
      or any later version published by the Free Software Foundation;
      with no Invariant Sections, no Front-Cover Texts, and no Back-Cover
	 Texts.  A copy of the license is included in the section entitled "GNU
      Free Documentation License".
</pre>
<p>
If you have Invariant Sections, Front-Cover Texts and Back-Cover Texts,
replace the "with...Texts." line with this: </p>

<pre>
    with the Invariant Sections being LIST THEIR TITLES, with the
    Front-Cover Texts being LIST, and with the Back-Cover Texts being LIST.
</pre>

<p>
If you have Invariant Sections without Cover Texts, or some other
combination of the three, merge those two alternatives to suit the
situation.</p>
<p>
If your document contains nontrivial examples of program code, we
recommend releasing these examples in parallel under your choice of
free software license, such as the GNU General Public License,
to permit their use in free software.
</p>

<hr />
<!-- <address> -->
<!--   <a href="mailto:rdiaz@ligarto.org">Ram&oacute;n D&iacute;az-Uriarte</a> -->
<!-- </address> -->


<!-- <hr /> -->

<!-- <p> -->
<!-- <a href="http://validator.w3.org/check?uri=referer"> -->
<!-- <img src="../valid-xhtml10.png" width="88" height="31" alt="Valid XHTML 1.0!" /></a> -->

<!-- <a href="http://www.anybrowser.org/campaign/">  -->
<!-- <img src="../anybrowser3.gif" width="88" height="31" alt="Viewable With Any -->
<!-- Browser" /></a> -->
<!-- </p> -->

<!-- </div> -->



<!-- </div> shouldn't this be the one for page?-->
</body>
</html>
