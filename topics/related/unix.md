## UNIX [draft]

### Resources

- [Art of Command Line](https://github.com/jlevy/the-art-of-command-line#processing-files-and-data)

### Find files

- `find dir -type f` Find all files in the directory   
- `find dir -type d` File all directories within this directory   
- `find dir -name “a*.mp3” -print0` Find all files/directory with name like a***.mp3   
- `find dir -type f -name “a*.txt”` Find all files (recursively) with name like a***.txt   
- `find dir -type f -print0 &#124; xargs -0 grep -l "word"` List file names with matching word. 
- `find dir -type f -print0 &#124; xargs -0 mv -t` Move all files from dir tree into single directory  

### Search in files

| command | action |
| --- | --- |
| grep “word” file | All matching lines |  
| grep -i “word” file | All matching lines - Ignore case |  
| grep -r “word” dir | All matching lines in all files or directory |  
| grep -c “word” file | Count of matching lines |  
| grep “word” file &#124; wc -l  | Count of matching lines |  
| grep -v “word” file | Count of non-matching lines |  
| grep -o -w “word” file &#124; wc -w | Word count |  
| grep -l -r “word” dir | List file names with matching word |  
| find dir -type f -print0 &#124; xargs -0 grep -l "word" | List file names with matching word. Find is fast, and can deal with file names with spaces and meta characters |


