---
layout: post
title:  "Tabularizing the Journal de Médecine Militaire"
date:   2021-04-23 00:00:01 -0500
categories: jekyll update
---
After cleaning the journal in the last post, it was time to organize the journal further and make tabular data from it. I decided to aim for a simple final product: isolating individual articles into rows. The data in each row would be separated by tabs to create a TSV file that I would then upload onto my GitHub repository. The first column would include the title. The second column would include all information relating to the author, and the third column would include the text of the article. Review Image One to see what the file looked like before this second round of cleaning. 
\
\
![Image One](https://raw.githubusercontent.com/Bengoff1/Images/main/Screenshot%20(54).png)
[Link_to_Image](https://raw.githubusercontent.com/Bengoff1/Images/main/Screenshot%20(51).png)
\
\
## Step One: Isolating Author Information. 
All authors were presented in journal in the following way: “Par M. (family name here)” to select those names I used the following expression `(Par|Par.)\sM\.`which looks for the word “Par” or Par followed by a period, then a space, then a capital M, followed by a period. Next, I added @@@ before each author using `@@@ Par M.` I now had a marker before each author. 
## Step Two:
## Isolating Titles
I had isolated title in a previous cleaning session, but I only put the word “Title” to act as a marker. I thought standardization in markers to be desirable, so this time I aimed to put @@@ in front of the titles. I modified a previously employed regex to find the first word of each title. \n(?=^[A-WYZÈ]{4,}) This regex looked for a line break that came before the start of an all capitalized word that was at least four characters long. I then used this regex `@@@\n` to add the three @ symbols in front of each title. 
## Step Three: 
## Isolating Text 
Each article ended with a period, and then a line break. To find these I used this expression `\.(?=\n)` and replaced it with this expression `\n@@@`. The difficulty here was that there were many periods that preceded a line break. So I had to look at each instance and decide if it was indeed the end of an article. I am sure a more complex regex could have automated this process for me. 
## Step Four: 
## Collapsing lines 
\
\
\
\
I then needed to get everything into place by collapsing the many lines into one single line. To do this I used `$` to put a `#` at the end of each line. Next, I used a `^` to put a # at the start of each line. I then employed the expression `#\n#` to find these line breaks. And replaced them with ##. This turned the document into a single line. 
Next, searching for the @@@, I added a break at the start of each article where the title was presented. Now each article was its own line. Next continuing to search for the @@@ I added a `\t` after the remaining @@@ symbols. The final step was to remove the @@@s and the ##s. I was left with one line for each article, and the internal components of each article were separated by tabs. See Image Two
\
\
![Image Two](https://raw.githubusercontent.com/Bengoff1/Images/main/Screenshot%20(55).png)
[Link_to_Image](https://raw.githubusercontent.com/Bengoff1/Images/main/Screenshot%20(52).png)
\
\
When I copied and pasted this into excel, a perfect table was the result. See Image Three, or visit my repository. 
\
\
![Image Three](https://raw.githubusercontent.com/Bengoff1/Images/main/Screenshot%20(56).png)
[Link_to_Image](https://raw.githubusercontent.com/Bengoff1/Images/main/Screenshot%20(53).png)
\
\
[Link_to_GitHub](https://github.com/Bengoff1/French_Military_Hospitals_1630_1815/blob/main/Journals/Journal_de_medecine_militaire/Tabularized_(2021_04_23)/JMM_Vol_1_Topo_Cleaned_TSV_Excel_(2021_04_23).txt)