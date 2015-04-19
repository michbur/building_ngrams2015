---
title       : Stepwise n-gram building
author      : Michal Burdukiewicz, Piotr Sobczyk
framework   : io2012 
highlighter : highlight.js
hitheme     : zenburn 
widgets     : mathjax       # {mathjax, quiz, bootstrap}
mode        : selfcontained
knit        : slidify::knit2slides
---

### Outline

1. n-gram definition.
2. Iterative n-gram building.
3. Results.
4. Conclusions and perspectives.


--- 



### n-grams (k-mers)

n-grams (k-tuples) are vectors of n characters derived from input sequence(s). They may form continuous sub-sequences or be discontinuous.  


Important n-gram parameter is its position. Instead of just counting n-grams, one may want to count how many n-grams occur at a given position in multiple (e.g. related) sequences.


--- 



### 1-grams


<!-- html table generated in R 3.1.3 by xtable 1.7-4 package -->
<!-- Sun Apr 19 22:11:20 2015 -->
<table border=1>
<caption align="bottom"> Sample sequences.  S - sequence, P - postion. </caption>
<tr> <th>  </th> <th> P1 </th> <th> P2 </th> <th> P3 </th> <th> P4 </th> <th> P5 </th> <th> P6 </th>  </tr>
  <tr> <td align="right"> S1 </td> <td> G </td> <td> A </td> <td> C </td> <td> T </td> <td> A </td> <td> A </td> </tr>
  <tr> <td align="right"> S2 </td> <td> G </td> <td> C </td> <td> G </td> <td> C </td> <td> A </td> <td> A </td> </tr>
  <tr> <td align="right"> S3 </td> <td> C </td> <td> C </td> <td> A </td> <td> C </td> <td> G </td> <td> G </td> </tr>
   </table>
  
&nbsp;
  
<!-- html table generated in R 3.1.3 by xtable 1.7-4 package -->
<!-- Sun Apr 19 22:06:41 2015 -->
<table border=1>
<caption align="bottom"> 1-gram counts. </caption>
<tr> <th>  </th> <th> A </th> <th> C </th> <th> G </th> <th> T </th>  </tr>
  <tr> <td align="right"> S1 </td> <td align="right"> 1 </td> <td align="right"> 2 </td> <td align="right"> 1 </td> <td align="right"> 2 </td> </tr>
  <tr> <td align="right"> S2 </td> <td align="right"> 2 </td> <td align="right"> 2 </td> <td align="right"> 2 </td> <td align="right"> 0 </td> </tr>
  <tr> <td align="right"> S3 </td> <td align="right"> 1 </td> <td align="right"> 0 </td> <td align="right"> 2 </td> <td align="right"> 3 </td> </tr>
   </table>

--- 

### 2-grams


<!-- html table generated in R 3.1.3 by xtable 1.7-4 package -->
<!-- Sun Apr 19 22:26:48 2015 -->
<table border=1>
<caption align="bottom"> Sample sequences.  S - sequence, P - postion. </caption>
<tr> <th>  </th> <th> P1 </th> <th> P2 </th> <th> P3 </th> <th> P4 </th> <th> P5 </th> <th> P6 </th>  </tr>
  <tr> <td align="right"> S1 </td> <td> G </td> <td> A </td> <td> C </td> <td> T </td> <td> A </td> <td> A </td> </tr>
  <tr> <td align="right"> S2 </td> <td> G </td> <td> C </td> <td> G </td> <td> C </td> <td> A </td> <td> A </td> </tr>
  <tr> <td align="right"> S3 </td> <td> C </td> <td> C </td> <td> A </td> <td> C </td> <td> G </td> <td> G </td> </tr>
   </table>
  
&nbsp;
  
<!-- html table generated in R 3.1.3 by xtable 1.7-4 package -->
<!-- Sun Apr 19 22:10:08 2015 -->
<table border=1>
<caption align="bottom"> 2-gram counts. </caption>
<tr> <th>  </th> <th> AA </th> <th> CA </th> <th> GA </th> <th> TA </th> <th> AC </th> <th> CC </th> <th> GC </th> <th> TC </th> <th> AG </th> <th> CG </th> <th> GG </th> <th> TG </th> <th> AT </th> <th> CT </th> <th> GT </th> <th> TT </th>  </tr>
  <tr> <td align="right"> S1 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 1 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 1 </td> <td align="right"> 0 </td> <td align="right"> 1 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 1 </td> <td align="right"> 0 </td> <td align="right"> 1 </td> </tr>
  <tr> <td align="right"> S2 </td> <td align="right"> 0 </td> <td align="right"> 1 </td> <td align="right"> 1 </td> <td align="right"> 0 </td> <td align="right"> 1 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 1 </td> <td align="right"> 1 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> </tr>
  <tr> <td align="right"> S3 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 1 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 1 </td> <td align="right"> 1 </td> <td align="right"> 0 </td> <td align="right"> 1 </td> <td align="right"> 1 </td> </tr>
   </table>

--- 


### 2-grams with position information


<!-- html table generated in R 3.1.3 by xtable 1.7-4 package -->
<!-- Sun Apr 19 22:26:48 2015 -->
<table border=1>
<caption align="bottom"> Sample sequences.  S - sequence, P - postion. </caption>
<tr> <th>  </th> <th> P1 </th> <th> P2 </th> <th> P3 </th> <th> P4 </th> <th> P5 </th> <th> P6 </th>  </tr>
  <tr> <td align="right"> S1 </td> <td> G </td> <td> A </td> <td> C </td> <td> T </td> <td> A </td> <td> A </td> </tr>
  <tr> <td align="right"> S2 </td> <td> G </td> <td> C </td> <td> G </td> <td> C </td> <td> A </td> <td> A </td> </tr>
  <tr> <td align="right"> S3 </td> <td> C </td> <td> C </td> <td> A </td> <td> C </td> <td> G </td> <td> G </td> </tr>
   </table>
  
&nbsp;
  
<!-- html table generated in R 3.1.3 by xtable 1.7-4 package -->
<!-- Sun Apr 19 22:27:57 2015 -->
<table border=1>
<caption align="bottom"> 2-gram counts. </caption>
<tr> <th>  </th> <th> X1_A.A_0 </th> <th> X2_A.A_0 </th> <th> X3_A.A_0 </th> <th> X4_A.A_0 </th> <th> X5_A.A_0 </th> <th> X1_C.A_0 </th> <th> X2_C.A_0 </th> <th> X3_C.A_0 </th>  </tr>
  <tr> <td align="right"> S1 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 1 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> </tr>
  <tr> <td align="right"> S2 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 1 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> </tr>
  <tr> <td align="right"> S3 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 0 </td> <td align="right"> 1 </td> <td align="right"> 0 </td> </tr>
   </table>


--- 

### Curse of dimensionality

$$n_{\text{max}} = p \times m^n$$

$n_{\text{max}}$: total number of n-grams.

$p$: number of possible positions.

$m$: number of letters in the alphabet.

--- 

### Curse of dimensionality

$$n_{\text{max}} = p \times m^n$$

![plot of chunk unnamed-chunk-7](assets/fig/unnamed-chunk-7-1.png) 


---

### More stuff

<!--html_preserve--><div id="htmlwidget-2655" style="width:504px;height:504px;" class="DiagrammeR"></div>
<script type="application/json" data-for="htmlwidget-2655">{ "x": {
 "diagram": "graph LR; A-->B; A-->C; C-->E; B-->D; C-->D; D-->F; E-->F" 
},"evals": [  ] }</script><!--/html_preserve-->

