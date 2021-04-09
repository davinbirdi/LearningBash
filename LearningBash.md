## How I am Learning to Cycle through screenshots:

First Need to list all files of interest in one location:
```
> cd ../Desktop
> ls Screen*

> mkdir Screenshots
> touch index
> ls -t *.png > index
```

This gives me all the names of the screenshots in one text file from newest to oldest.
To prove that I have this, I can:
```
> cat index
```
Which will print out all the contents of the file index into the standard output
I can now read each line of the file and then determine if I want to delete it.
```
> read line < index; echo $line
```
This prints out the first line from the file index.
I can modify this to open the file (where the name is stored in the variable $line).
```
> read line < index; open $line
```
If I want to delete the file, I can type:
```
> rm $line
> ls -t *.png > index
```
Which deletes the file and updates the index file.

If I want to keep the file, I can type:
```
> mv $line ..
> ls -t *.png > index
```
Which moves the file to the parent directory and updates the index file.

This accomplished most of what I want to do to clean up my screenshots that i've saved.


I want to take this a step forward in that I don't have to type the commands out each time,rather only press "y/n" as I check the contents of each file.
** Note: This actually deletes things instead of throwing to trash/recycle bin.



Making a bash script:

So big learning is when I create a variable that has special characters in it ("/ " for space), I have to use double quotes when calling it.
This is because when I call "read -r line < index", I'm specifying raw input.

When calling it, I also have to specify raw input, otherwise the the command sees it as "Screen/ Shot/ 1/ etc.png" and separates the input everytime it sees the space.

By using double quotes in cases like:
```
> open "$line"
```
The interpreter (? or console) gets that I want to read it as is, accepting special characters like space.


Another problem; closing the open Preview Application that is showing us the screenshot.
Found this online:
```
> osascript -e 'quit app "APPLICATIONNAME"'
```
Keeping the command window ontop/in focus:
```
> open -g
```


In total, the entire script is as below:

