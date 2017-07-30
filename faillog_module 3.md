# Module 3: Fail log
## July 23 2017

### Exercise 1
+ downloaded correspondence of Republic of Texas for 1911 using curl command (`$ curl http://archive.org/stream/diplomaticcorre33statgoog/diplomaticcorre33statgoog_djvu.txt > texas.txt`)
+ following instructions, deleted all but letter index
+ used regex to remove all but lines containing letters
+ `sed -r -i.bak -'s/(,)( [0-9]{4})(.+)/\2/g' index.txt`
 + got an error message, but index.txt looks fine in nano, so I retry the sed command
 + typing it in more carefully works - the `-` before `'s/...'` was the problem. hurrah!
+ tried to remove tildes with `sed -r -i.bak 's/\n~//g' index.txt` - didn't work - tried with `sed -r -i.bak 's/~//g' index.txt` did work
+ changed " to" to "," with `sed -r -i.bak 's/ to\b/,/g' index.txt`
+ grep is not printing to screen?
 + tried a few searches ('Burnet,' 'Allen') and got results - including the line mentioned in the workbook as having an extra comma - apparently there are no lines with extra commas in this version?
  + Thinking I may have gotten the regex wrong, I started going to a backup by renaming index.txt to index_oops.txt, then making a new index.txt
  + then I double-checked with Dr. Graham's regex - mine was the right command, and line 178 definitely has 3 commas, so the problem is with my grep command, not my sed commands. I turned index_oops.txt back into index.txt and posted on slack about grep.\
+ redid the exercise in Cygwin and got `grep -E ".+,.+,.+,"` index.txt to return results :) 
+ used ^W in nano to find and correct 13 lines of text.
+ made new command history and saved as module3exercise1_commands_cygwin.md.
+ uploaded module3exercise1_commands.cygwin.md and cleaned-correspondence.csv to github repo /hist3814o_module3/.
+ doing this exercise again after playing with the Equity helped me understand how exactly I can apply the regex patterns I've been applying to find days of the week in Equity to creating a usable CSV. I'm on my way!
 
 ### Exercise 2
 + since I couldn't finish exercise 1, I started exercise 2 with [Thomas Palladia's OpenRefine tutorial](http://thomaspadilla.org/dataprep/).
  + I installed OpenRefine and did basic clustering cleanup & whitespace removal on the British Library's [CSV of comic publications](http://www.thomaspadilla.org/data/dataprep/)]
   + without the intention to use this file for much, I was kind of lazy on the transformations. For example, if a cell contained 2 publication dates (such as `1991 c1992` or `[1991], 1992`) I just chose the first date listed.
  + exported as module3exercise2.csv for upload to Github.
+ couldn't access DHbox to make the .csv from exercise 1 (& didn't really feel like redoing the exercise in Notepad++). To pass time, I downloaded the [Named Entity Extraction](http://freeyourmetadata.org/named-entity-extraction/) plugin.
 + extractd named entities in "Place of Publication" column. VERY slowly...
  + These results are so cool! I can't wait to use this for visualization.
+ cleaned up my cleaned-correspondence.csv
 + extracted named entities in senders, because why not.
  + funny fail: it extracted names as place names, eg Sam Houston became Houston. Close but no cigar. I deleted the extraction column and moved on with the exercise.
 + changed to 2-column csv with "sender" changed to "source" and "recipient" changed to "target" for visualization. saved at module3exercise2_returnofthecommandline.csv.
+ loaded csv into [Palladio](http://hdlab.stanford.edu/palladio-app/) and played around. Sam Houston wrote & recieved a lot of letters. I saved one graph I generated as module3exercise2_texasgraph.svg.
+ uploaded .csv and .svg files to github.
 
### PROJECT WORK
+ still unable to access dhbox, I downloaded 83471_1890-01-02.txt (Equity issue for the 2nd of January 1890) and played around with regex cleaning in regexr and Notepad++.
+ trying to isolate proper nouns (words starting with capital letter...) `(\b[A-Z].+[^\s])`??
 + `\b[*. ][A-Z][a-z|A-Z]*` returns all capitalized words not at the beginning of a sentence
+ could I find all instances of dates WITHIN ARTICLES and use those to examine what kinds of events happened?
 + first must remove all non-article material (eg headers containing dates of publication)
 + could I extract the words AROUND each date, then use that to find what kinds of events were run? extract each LINE with a DAY in it? (sunday, monday, tuesday...)
 + went thru Equity for 2 January 1890 using `[A-Za-z]*day` regex  (note: not perfect - returns results for "today" and "holiday", etc; because I'm just playing around manually right now I just skip past those results - if I were to sed or grep something, I'd need to be more specific) and put in experimental XML tags: `<event>`, `<eventDate>`, and `<location>` for each social gathering referred to by day of event
  + could I later use these XML tags to create a csv like so: event, date, location, date of mention in Equity???
   + OOH!
+ I refer to my final project github repo to check what my ideas actually were...
 + hyperlinking: could I look for repeated words/events & hyperlink them together?
  + what [larger historical argument](http://scottbot.net/argument-clinic/) could this serve?
+ started adding `<div>`, `<dateline>` and `<p>` tags to 2 Jan 1890 issue (according to [TEI guidelines](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/DS.html)). Realized that this is a lot of work, and I probably won't be data mining this version of the text as DHbox still isn't up, so I stop a few stories in.
 + it's almost impossible to `<div>` some of these (eg the OCR for 9 January 1890) properly because of the way the OCR read the text across columns.... great.
 + looking into downloading Cygwin so I can do some greping and seding on my Windows machine. Good idea or no...?
+ can find instances of dates when properly spelled with regex `\b.+(Mon|Tues|Wed|Thurs|Fri|Satur|Sun)day.+`
 + problem: won't find split words or badly OCR'd words.
 + problem: `.+day.+` returns all lines with "day," "today," "holiday"...
+ observation: the word "left" seems to appear a lot with "___day" words. Maybe there IS nothing to do in Shawville - everyone is always leaving...
+ observation: why are some issues OCR so different? the OCR for Jan 02 is very readable compared to Jan 09.
+ tried combining commands from exercise 1 (using a tilde to isolate relevant lines) with my sed commands designed to find days. not very useful - too much info gets cut off due to bad OCR. still, I saved a grep example of lines containing pattern `.+day\b.+` as 05-07-1891-days.txt to see.
+ uploaded files mentioned in this section to /hist3814o_finalproject/ repo.
