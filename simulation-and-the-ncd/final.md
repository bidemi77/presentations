
<!--- SET THE URL OF YOUR PRESENTATION. ---> 
<!--- THIS WILL LOOK LIKE https://norfolkdatasci.github.io/presentations/YOUR-PRESENTATION-NAME-HERE --->
<meta property="og:url" content="https://norfolkdatasci.github.io/presentations/simulation-and-the-ncd">

<!--- MAKE THE TITLE THE SAME FOR THESE 2 METATAGS --->
<meta name="twitter:title" content="When is simulation better than analysis?">
<meta property="og:title" content="When is simulation better than analysis?">

<!--- MAKE THE COVER IMAGE THE SAME FOR THESE 2 METATAGS --->
<meta property="og:image" content="https://raw.githubusercontent.com/NorfolkDataSci/simulation-and-the-ncd/master/thumbnail.png">
<meta name="twitter:image" content="https://raw.githubusercontent.com/NorfolkDataSci/simulation-and-the-ncd/master/thumbnail.png">

<!--- MAKE THE DESCRIPTION THE SAME FOR ALL THESE METATAGS --->
<meta name="description" content="A discussion of when is simulation better than analysis" />
<meta name="twitter:description" content="A discussion of when is simulation better than analysis">
<meta property="og:description" content="A discussion of when is simulation better than analysis" />

<!--- DONT TOUCH THESE METATAGS --->
<meta name="twitter:card" content="summary">
<meta name="twitter:site" content="@NorfolkDataSci">
<meta property="og:site_name" content="Norfolk Data Science" />
<meta name="twitter:creator" content="@NorfolkDataSci">
<meta property="og:type" content="website">

<!--- CHANGE TO THE FILE PATH OF YOUR PRESENTATION IN THE REPOSITORY --->
<!--- The file path will look something like https://github.com/NorfolkDataSci/presentations/tree/master/YOUR-PRESENTATION-NAME --->
<a href="https://github.com/NorfolkDataSci/presentations/tree/master/simulation-and-the-ncd"><img style="z-index: 1000; margin: 0px !important; max-height: 300px !important; position: absolute; top: 0; right: 0; border: 0;" src="https://camo.githubusercontent.com/38ef81f8aca64bb9a64448d0d70f1308ef5341ab/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6769746875622f726962626f6e732f666f726b6d655f72696768745f6461726b626c75655f3132313632312e706e67" alt="Fork me on GitHub" data-canonical-src="https://s3.amazonaws.com/github/ribbons/forkme_right_darkblue_121621.png"></a>

<!--- DONT TOUCH --->
<div class="logo">
  <a href="http://www.meetup.com/NorfolkDataSci" target="_blank">
    <img src="../norfolk-data-sci-logo.png" style="width:200px;" alt="logo" />
  </a>
</div>

<!--- DONT TOUCH --->
<div class="copyright">
  Norfolk Data Science: 
  <a href="http://www.meetup.com/NorfolkDataSci/" target="_blank">
    http://www.meetup.com/NorfolkDataSci
  </a>
</div>


When is simulation better than analysis?
========================================================
author: Roy W. Wilson
date: March 7, 2017
css: ../norfolk-data-sci-presentations.css
autosize: true

This presentation is abstracted from my 2007 paper at <http://jasss.soc.surrey.ac.uk/13/3/8.html>



What about moi? (1/13)
========================================================
<ul style="padding-top:10px;">
<li style="padding-top:10px;">Undergraduate majors in Mathematics and in Philosophy</li>
<li style="padding-top:10px;">Masters degrees in Mathematics and in Computer Science</li>
<li style="padding-top:10px;">Used math/stats/simulation on a national intelligence project
  <ul style="padding-left: 40px;padding-top:5px;">
    <li>Held an SCI clearance</li>
  </ul>
</li>
<li style="padding-top:10px;">Graduate minor in statistics
  <ul style="padding-left: 40px;padding-top:5px;">
    <li>Non-parametrics, SEM, Experimental and Quasi-Experimental Design</li>
  </ul>
</li>
</ul>

A Minimal Social Network (2/13)
=========================================================

Suppose two people ($x$ and $y$) meet to work on a problem knowing nothing about each other. 
After brief discussion, it seems that $x$ knows more than $y$ about something that seems 
relevant to the problem. A relationship of dominance might then form between $x$ and $y$, 
a situation that can be represented as $xDy$.
<br/>
<br/>
For simplicity, suppose that: if $xDy$, then $ydx$ where $d$ indicates that $y$ defers 
to $x$, and; once a social relationship forms between $x$ and $y$, it remains through 
the remaining sequence of interactions. 

A model of a larger network (3/13)
========================================================

This initial *DISCRETE* state of the social situation involving four persons can 
be pictured as the 4 x 4 sociomatrix $R$:


```
     [,1] [,2] [,3] [,4]
[1,] "u"  "u"  "u"  "u" 
[2,] "u"  "u"  "u"  "u" 
[3,] "u"  "u"  "u"  "u" 
[4,] "u"  "u"  "u"  "u" 
```
where 'u' (for 'undefined') indicates that a task-related social relationship is not (yet) defined.

A Formal Structure - Part 1 (4/13)
========================================================

Now, suppose that, after some discussion, it seems that Agent 4 has (or seems to have) 
more task-relevant knowledge than the others. At least for a while, the other three 
agents may defer to Agent 4 when trying to define (or carry out) the task, a situation 
formally represented as:


```
     [,1] [,2] [,3] [,4]
[1,] "u"  "u"  "u"  "d" 
[2,] "u"  "u"  "u"  "d" 
[3,] "u"  "u"  "u"  "d" 
[4,] "D"  "D"  "D"  "u" 
```

The Formal Structure - Part 2 (5/13)
========================================================

If at time $i$, a pair of members interact, a new social relation *MAY* form, 
thereby generating $R[i+1]$. With "enough" interactions, say $K$, every off-diagonal 
entry of $R[K]$ is either d or D. For example, with $K = 6$ interactions we might have:


```
     [,1] [,2] [,3] [,4]
[1,] "u"  "d"  "D"  "D" 
[2,] "D"  "u"  "d"  "D" 
[3,] "d"  "D"  "u"  "d" 
[4,] "d"  "d"  "D"  "u" 
```

SO WHAT? (6/13)
=========================================================

<br/>
Suppose that it was, in fact, a simulation that transformed $R[0]$ to $R[6]$.
<br/>
<br/> 
Might there be some other method not involving simulation that is simpler and/or quicker? As always, it depends.

Is R[6] predictable from R[0]? (7/13)
========================================================

The Incompressibility Criterion 
<div style="margin-top: -10px;">
"formulates the unpredictability of a given state from knowledge of the rule and initial state ... — but of course, not [emphasis added] of step $n + 1$ relative to step $n$, since this is perfectly … determined."
</div>

(Huneman, 2008, p. 600)

An object $o$ is INCOMPRESSIBLE if $C(o)$, the length of a compressed version of $o$ obtained via some real-world compressor $C$, and the length of $o$, denoted $len(o)$, are related as follows (where $C(o)$ and $len(o)$ are defined in terms of bits):
<br/>
<br/>
$C(o)$ > $len(o)$ (Li and Vitanyi 2008, p. 116).

Using the Incompressibility Criterion (8/13)
====================================================

* Formal inference about COMPRESSIBILITY (and, therefore, INCOMPRESSIBILITY) is based on Kolmogorov complexity (which is related to, but distinct from, Shannon complexity). 
* The Kolmogorov complexity function is not itself computable, but it can be approximated by real-world compressors such as zip, bzip, and pmz. 
* One such approximator is the Normalized Compression Distance function $NCD()$ (<http://complearn.org/ncd.html>).
<br/>
<br/>
Can we use it to analyze the (sequence) $R[i]$?

Step 1: map each R[i] to a string S(i) (9/13)
========================================================


```
     [,1] [,2] [,3] [,4]
[1,] "u"  "d"  "D"  "D" 
[2,] "D"  "u"  "d"  "D" 
[3,] "d"  "D"  "u"  "d" 
[4,] "d"  "d"  "D"  "u" 
```

$R[6]$ becomes $S(6)$:


```
 S(0):  uuuuuuuuuuuuuuuu 
 S(1):  uuuDuuuuuuuuduuu 
 S(2):  uduDDuuuuuuuduuu 
 S(3):  udDDDuuuduuuduuu 
 S(4):  udDDDududDuuduuu 
 S(5):  udDDDudDdDuudduu 
 S(6):  udDDDudDdDudddDu 
```

Step 2: Compute NCD(S[i-1],S[i]) (10/13)
========================================================

1. The first row, "I", identifies each member of the ${S[i]}$ sequence shown on the previous slide. 
2. The second row, "C", shows the number of bits in the compressed version of each $S[i]$.
3. The third row, "NCD", shows $NCD(S[i-1],S[i])$, where $i$ = 1 ... 6.


```
                                            
I      0    1    2    3     4      5       6
C     88  136  144  144   176    192     168
NCD <NA> 0.53 0.32 0.37  0.48   0.44    0.32
```

Interpreting the previous table (11/13)
=======================================================================

For $i$ > 0, $S[i]$ is an incompressible sequence of characters *BECAUSE* $C(S[i])$ > 128 = $len(S[i])$ = 16 * 8. 

Typically 0 ≤ $NCD(a, b)$ < 1.1. The smaller the value of $NCD(a, b)$, the greater the similarity between $a$ and $b$. The first state transition from $R[0]$ to $R[1]$ generates more unpredictable than any succeeding state transition. Yet, dissimilarities accumulate:<br/>
$NCD(S[0], S[6]) = 0.64$ > $NCD(S[i],S[i+1])$ for all $i$ > 1.  


Summary (12/13)
========================================================

My (hypothetical) agent-based simulation transforms the COMPRESSIBLE macrostate $R[0]$ into the INCOMPRESSIBLE macrostate $R[6]$. Yet, a different set of rules/representations might generate a different sequence of network states. This *MIGHT* make it possible to get from an equivalent final state to an equivalent final state in fewer steps. 

BTW, there is a problem with my use of the $NCD$.<br/><br/>Any thoughts?

Possibilities (13/13)
=======================================================

Given specified initial and target network structures, an $NCD$ calculation might indicate the difficulty of predicting (by data science) whether the network might so evolve.

The Norfolk Data Science repository includes a [2015 paper by Cohen and Vitany](https://cdn.rawgit.com/NorfolkDataSci/presentations/39342a11/simulation-and-the-ncd/nihms644361.pdf) that extends the scope of the $NCD()$ to multisets and applies it to Optical Character Recognition. 

I am best as a scout/explorer and seek short-term projects.
