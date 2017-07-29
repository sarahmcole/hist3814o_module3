# HIST 3814O MODULE 3 EXERCISE 1: PART II: THE RETURN OF THE COMMAND LINE
## July 28 2017

This is my command history using cygwin to complete exercise 1 of module 3, 
which I had already done up to step 5 (cleaning up the text) when I got 
stuck and DHBox went down.

The log starts at 29 because Cygwin saved all my commands from my last 
session as well - which is good to note for the future, given my habit of 
forgetting to save my command history.

   29  cd module3exercise1
   30  curl http://archive.org/stream/diplomaticcore33statgoog/diplomaticcore33statgoog_djvu.txt > texas.txt
   31  nano texas.txt
   32  nano texas.txt
   33  nano texas.txt
   34  nano texas.txt
   35  nano texas.txt
   36  sed -r -i.bak 's/(.+\bto\b.+)/~\1/g' texas.txt
   37  grep '~' texas.txt > index.txt
   38  nano index.txt
   39  sed -r -i.bak 's/(,)( [0-9]{4})(.+)/\2/g' index.txt
   40  sed -r -i.bak 's/~//g' index.txt
   41  nano index.txt
   42  grep -E ".+,.+,.+," index.txt
   43  sed -r -i.bak 's/ to\b/,/g' index.txt
   44  grep -E ".+,.+,.+," index.txt
   45  nano index.txt
   46  cp index.txt cleaned-correspondence.csv
   47  history > module3exercise1_commands_cygwin.md
