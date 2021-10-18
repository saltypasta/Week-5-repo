---
tutorial:
date: 2021-10-16
tags: tag1, tag2, etc
---

# what I was trying to do

_Modify the existing scheme/suggest new category for kobotoolbox form. Get  my feet wet with R 

+ `[Week 5 Repo](https://github.com/saltypasta/Week-5-repo)`

## how it might connect to other research I'm doing

_Adjusting the form will further understanding of "what gets counted counts", Using R will hopefully provide insight into what kind of analysis we can accomplish, as well as how our decisions around data collection manifest in the analysis stage

## what I did

+ ####  Kobotoolbox
	+ registered, imported the form and began editing. Took screenshots as I went
	+ See Form Edit Screenshots folder for some minor edits I added, mostly to accommodate working from digital images instead of graves
	+ Unsure how how to implement the following Idea on Kobo but I will try and describe/illustrate it here:
		+ For the shape of graves, one method that may be more accurate is allowing the recorder to digitally "trace" the outline of a gravestone. This is in the same vein as our photogammetry unit but a bit more simple. 
		+ For example, take this [gravestone](obsidian://open?vault=obsidian-digiarch-lab-notebook-main&file=Week%205%2FGravestone%20Ex..jpeg)
		+ Using that reference image, I traced the outline of the stone and any text boxes that appeared like [so](obsidian://open?vault=obsidian-digiarch-lab-notebook-main&file=Week%205%2FEdited%20Gravestone%20Ex..JPG)
		+ In theory, if we recorded all our gravestones with a program that allowed us to trace the shape of the stones, textboxs, motifs etc. we would be able to accurately record that data without having to classify it into arbitrary groups. 
		+ Additionally, this would allow for visual analysis of the shape of the stones. one way I can think of would be to overlay or average the line data based on a specific parameter such as "Date of construction"
		 + This would reveal visual trends in the shapes of the stones overtime. an example of lines taken from 5 stones overlayed may look like [this](obsidian://open?vault=obsidian-digiarch-lab-notebook-main&file=Week%205%2FGrave%20Lines%20Overlay%20Ex.JPG)
		 + visualizing the data this way allows us to see visual trends in the sample of graves we select. This method also depicts each stones shape accurately instead of lumping them into arbitrary categories
		 + There are problems with this method, such as finding/learning a program that can allow the user to sketch/record the models, as well as arrange them in a way that is meaningful to us
			 + This also increases the chance of user error such as having an open ended shape resulting in an incomplete or broken entry, drawing poor quality/lazy lines, or mixing up the textbox and grave categorizations. 
			
+ #### R
	+ Launched virtual version of R after reading the issues folks had with the PC version in discord
	+ Made new script
	+ Downloaded script file, opened it with a text editor
	+ ran install.packages("archdata")
		+ lots of lines appeared in console, finished with done sooooo it worked?
	+ Ran library(archdata)
		+ nothing happened?
	+ Ran library(RcmdrMisc)
		+ Loading required package: car Loading required package: carData Error: package or namespace load failed for ‘car’ in dyn.load(file, DLLpath = DLLpath, ...):
 unable to load shared object '/srv/conda/envs/notebook/lib/R/library/Rcpp/libs/Rcpp.so':
  /usr/lib/x86_64-linux-gnu/libstdc++.so.6: version `GLIBCXX_3.4.26' not found (required by /srv/conda/envs/notebook/lib/R/library/Rcpp/libs/Rcpp.so) Error: package ‘car’ could not be loaded
  
  + Ill try running that all together I guess?
	  + Didnt work, same error

+ try adding install. infront of library(archdata)
	+ Error in install.library(archdata) : 
  could not find function "install.library"
  
 + maybe I dont need to run the library(archdata) and library(RcmdrMisc) lines? Ill try going to the next step
 + ran ??archdata and it showed up in blue in the console... I assume that is good?
 + Ran data(DartPoints) and View(DartPoints) and a new tab opened! 
 + Ran mean(DartPoints$Length) and got 49.33077
 + tried to run options(digits=3) and numSummary(DartPoints[, 5:11])
	 + Error in numSummary(DartPoints[, 5:11]) : 
  could not find function "numSummary"
  + Try again with just Summary(DartPoints[, 5:11])
	  + Error in (function (classes, fdef, mtable)  : 
  unable to find an inherited method for function ‘Summary’ for signature ‘"data.frame"’
  + Googled, and found the following response for that error:
	  + That is the type of message you will get when attempting to apply an S4 generic function to an object of a class for which no defined S4 method exists (or at least has been attached to the current R session).
+ No idea where to proceed from there, Ill move on to the next step and #revisit	this later
+ ran table(DartPoints$Name)
	+ got: Darl      Ensor  Pedernales     Travis      Wells 
        			28         10         32                   11         10
+ Ran prop.table(DP_Type)*100
	+ Darl      Ensor Pedernales     Travis      Wells 
      30.8       11.0       35.2       12.1       11.0
+ Ran (DP_CT <- xtabs(~Name+Blade.Sh, DartPoints))
+  Blade.Sh
Name          E  I  R  S
  Darl       15  2  0 10
  Ensor       2  1  0  6
  Pedernales 15  1  3 13
  Travis      7  0  0  4
  Wells       3  0  0  7
  + Ran addmargins(DP_CT)
	  +  Blade.Sh
Name          E  I  R  S Sum
  Darl       15  2  0 10  27
  Ensor       2  1  0  6   9
  Pedernales 15  1  3 13  32
  Travis      7  0  0  4  11
  Wells       3  0  0  7  10
  Sum        42  4  3 40  89
  + Ran dim(DartPoints)
	  + Got 91 17, same as the tutorial 
+ ran View(DartPoints)
	+ located missing cells that had N/A as an entry

+ ran addmargins(xtabs(~Name+addNA(Blade.Sh), DartPoints))
	+  addNA(Blade.Sh)
Name          E  I  R  S <NA> Sum
  Darl       15  2  0 10    1  28
  Ensor       2  1  0  6    1  10
  Pedernales 15  1  3 13    0  32
  Travis      7  0  0  4    0  11
  Wells       3  0  0  7    0  10
  Sum        42  4  3 40    2  91
	
	
+ so just about everything ran fine, next step is to add another dataframe? 
+ Going to leave it here. can #revisit later, maybe try and make it further for the consolidation doc. 



## challenges 
Listed error messages and resources in steps. 

## thoughts on where to go next
Will reach out to discord to try and get further with R before the consolidation doc
