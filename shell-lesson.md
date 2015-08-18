## Working in the Shell:

Data source:  https://github.com/tracykteal/data-years ("Download zip")
    Download the data-years-master zip file from that location
    Open your shell (in mac, this is Terminal program in Applications)
        in Windows, you should have downloaded Git bash
        
In your shell you first have to locate yourself in the file system. 

```
$ pwd   (tells you where you are)
$ cd       (by itself cd brings you home)
$ ls       (lists all the files in your current folder)
$ cd Downloads   (takes you into a Downloads folder if it is in the current directory)
$ ls
``

find the folder data-years-master   (if it is still a zip, then you have to unzip it)


    $ unzip data-years-master.zip


This will create a folder named data-years-master that is filled with a bunch of csv files. Note that you should usually put the file in its own folder before unzipping just in case it doesn't have its own folder inside of it.

```    
$ cd data-years-master
$ ls    (should list a bunch of csv files like 1977-data.csv)
$ less 1977-data.csv    (this will let you browse the file, hit SPACE to look at more)
``` 

- hit G to go to end of file
- hit q to quit the file

To learn more, google "unix less" (or any other command).
Wikipedia has very friendly pages for these commands.

To find something within less, hit / followed by your search phrase.

TAB complete works in the shell too - will attempt to finish a file name
if there is more than one that completes what you have typed, hit TAB again
this lists the potential files names that fit.

    $ head 1977-data.csv   (prints first 10 lines of the file)

### Exercise
Print just the first line of the file

    $ head -n 1 1977-data.csv   (in this case shows headers)

How to see headers of all the files?

    $ head -n 1 *.csv    (dumps file name and then first line of file for all .csv files)

* is a wildcard that matches anything, so *.csv matches all files that end in .csv.  
But it scrolls by too fast

    $ head -n 1 *.csv | less   

Does the same thing but "pipes" the results to less using the | so you can browse the results
    
But you want to put them into a file

    $ head -n 1 *.csv > all-years-headers.txt   

Sends the results to a file using > now you can look at it

    $ wc 1977-data.csv   

Gives word count for file, here words are defined by spaces.
So this file has same number of words as lines but we were lucky

    $ wc -l 1977-data.csv   (the -l parameter gives lines directly)

careful: the line count is the number of entries + 1 (for the header)

### Exercise

Put all years entry counts into a file

```
$ wc -l *.csv > entries     (puts all entry counts for the csv files into a file called entries)
>> appends to an existing file
```

Combine all the data into one file:
    $ cat *-data.csv > all_things     

Concatenates all the files into one.  The problem with this is the headers are included in the resulting file.

Control c gets you out of a command you are stuck in.

Get the header:
    $ head -n 1 1977-data.csv > alldata

Append the data from all the files using a for loop:

    $ for filename in *-data.csv; do tail -n +2 $filename >>alldata.csv