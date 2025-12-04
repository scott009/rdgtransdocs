# Tasks


### Task 1
- Task Date 11/27/2025
Examine the html documents in winoutput/doc
  
  
Do not commit to remotes until tell you too
create a copy of  engweb in winoutput/docs and nameit rdgBook2.html 
lets use this to optimize our html structure so that it is rigourousl semamtic  
  
Phase 1: Fix Hierarchy (now) ✓ Correct approach
  - Add <h1> for book title
  - Remove all <h3 class="id-tag"> misuse
  - Move IDs to id attributes on <p> elements
  - Ensure proper heading nesting (<h1> → <h2> → <h3> only for actual headings)
    
now repeat this process for thai   
create a copy of rdgThai.html in winoutput/docs and name it rdgThai2.html   
modify it using the same methodes you used to create rdgBook2.html  
once its dome you can commit it to the remote   
but don't do any other languages yet. 




### Task    2
- Task Date 11/27/2025
Create the first Thai translation master 


I want to create and html document   called tmasterThai.html

#### inputs
It will have several inputs 
- jmaster - for structural guidance 
- engmaster - english language sour- ce document 
- engweb - the look and feel should be based on this 
- stylefile - use this as to style the tmasterThai    
- thaisrc:  rdgThai2.html  
engsrc: rdgBook2.html

#### output
**tmthai**:  tmasterThai.html
##### Description 
 tmthai will have 2 entries for each paragraph 
What is a translation master 

A translatoin mater is an html document that   is intended to aid human bilingual readers correct and comment 
on the AI translations 

tmasterThai.html contains  a very large webform,
For each each paragraph in the in thaisrc
there is a matching paragraph in engsrc
The Thai content is enclosed in a text area which the user can edit to correct the translation. 

When they are done. they push the submit button.   
it is preferred that the resulsts are enclosed in a appropriate json file  
The goal is to have corrections that are natural and easy to integrate back into jmaster (for staus updates)   
and to correct the appropriate md file down the line. 
/home/scott/gitrepos/rdgtrans/lmasters/RDGBook_Thai.md 

for the moment we are limited to the capabiites of github pages. 
but lets discuss this before doing this. 
=================
● Perfect! Let me rewrite the script to use workmaster.json as the structural guide:
next 

create Japaesee

## Task 3 
complete version one based on the local Thai Tmaster file 
But add version 1 to the header     


## Task 4(Complete)
version 2 
add languge text  to the form   
in a way this is form page metta data   
"Recovery Dharma - Thai Translation Correction Tool"  should have matching strings in the target language.   
  
Rather than doing this directly, create a seperate file with the string   
and a tranlation in each target language. 
reading this file (it might be a Json ile wile become part of the process of creating the tmasters 

## Task 5  (completed)
Create a table of Documents HTML file 

## Task 6  (Complete )
embed the audio
The first thing to know is that I have added audio files to archive.org  
I have created a new html file
C:\Users\scott\Documents\RecoveryDharma\RDGBook\output_V1\docs\rdgtranslations2.html   
Lets start wwith English and then move on to thai
here are the urls for the mp3 versions
https://archive.org/download/rdgtbooktranslations/ChineseSimplified_Introductions.mp3
https://archive.org/download/rdgtbooktranslations/ChineseTraditional_Introductions.mp3
https://archive.org/download/rdgtbooktranslations/English_Introductions.mp3
https://archive.org/download/rdgtbooktranslations/Korean_Introductions.mp3
https://archive.org/download/rdgtbooktranslations/Thai_Introductions.mp3
https://archive.org/download/rdgtbooktranslations/Vietnamese_Introductions.mp3
https://archive.org/download/rdgtbooktranslations/Japanese_Introductions.mp3
  
  [rd-translations](https://bit.ly/rd-translations)

=============
## Task 7 (Complete)  
- use serverless functions to store json results on github
- store form output in a repository   the repository is  **corrections**  
detailed documentation in Netlify.md

## Task 8  (next Task)
use the presentation layer json to update documents to add target translation lanuges 
There are 2 steps to this task
### Step A Update presentation.json    
understatnd that it is in the **showoff** structure in Opguide
Limit intitial work to tmasterThai.html and presentation.json
#### A.1 (complete)
- Scan the contents of  tmasterThai.html paying particular attention to the element class names 
-  Create an element list of them and save it  **dochome* and call it elementlist.md and wait for discussion 
#### A.2   
- Do not advance to this step until I tell you we are ready.!
  for each element list item:
    populate presentation.json  with a json object. 
    The object will have a element name (in English)  
    A value for English and each of the target translation languages
  - make sure that, in each of these objects   the value of the traget language is always correct. 
### Step B Update tmasterThai.html      
- Do not advance to this step until I tell you we are ready.!
- Make sure to limit this to tmaster.Thai.html  
In this step we will add a button totmasterThai.html that will toggle  the values of all the labels from 
English to the target translation language.   
There will be a process of review and fine tuning before we propagate to the rest of the system 
I will add more detailed instructions once we reach reach this step 

  file:///C:/Users/scott/Documents/RecoveryDharma/RDGBook/output_V1/docs/tmasterThai.html


