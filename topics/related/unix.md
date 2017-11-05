## UNIX

### Resources

- [Art of Command Line](https://github.com/jlevy/the-art-of-command-line#processing-files-and-data)

### Table of Contents

  * [Resources](#resources)
  * [Find](#find)
  * [Search](#search)
  * [Processes](#processes)
  * [File permissions](#file-permissions)
  * [List files](#list-files)
  * [Symlinks](#symlinks)
  * [Checking logs](#checking-logs)
  * [Text manipulation](#text-manipulation)
  * [Sed](#sed)
  * [Networking](#networking)
  * [Space](#space)
  * [Miscellaneous](#miscellaneous)


### Find

- `find dir -type f` Find all files in the directory   
- `find dir -type d` File all directories within this directory   
- `find dir -name “a*.mp3” -print0` Find all files/directory with name like a***.mp3   
- `find dir -type f -name “a*.txt”` Find all files (recursively) with name like a***.txt   
- `find dir -type f -print0 | xargs -0 grep -l "word"` List file names with matching word
- `find dir -type f -print0 | xargs -0 mv -t` Move all files from dir tree into single directory  

### Search

- `grep “word” file` All matching lines in the file   
- `grep -i “word” file` All matching lines - Ignore case   
- `grep -r “word” dir` All matching lines in (recursively) all files or directory   
- `grep -c “word” file` Count of matching lines   
- `grep “word” file | wc -l` Count of matching lines   
- `grep -v “word” file | wc -l` Count of non-matching lines   
- `grep -o -w “word” file | wc -w` Word count   
- `grep -l -r “word” dir` List file names with matching word   
- `find dir -type f -print0 | xargs -0 grep -l "word"` List file names with matching word 

### Processes

- `nohup program.sh > mylog.txt 2>&1 &` 
    + `&` starts process as child process in the background
    + `nohup` Ctrl-C or terminating session sends kill signal to all child processes, `nohup` catches and ignores it
    + `>` redirect output (from left/source to right/target)
    + `2` error stream
    + `1` output stream 
    + `2>&1` append all errors to output
- `top` Check CPU and memory consumption
- `kill -9 processId` kill the process with that pid
- `kill -3 processId` for a JVM process, will write thread dump to output stream
- `ps -ef | grep word` find process with matching word
- `echo $?` print output of last process

### File permissions

- `chmod file` Change 
- `chmod +x file` Add execute permission
- `chmod +w file` Add write permission
- `chmod +r file` Add read permission
- `chmod 755 file` Change permission
- `chmod -R 755 dir` Change permission recursively
- `chmod g+w file` Add write permission at group level
- Numbers: 1=x, 2=w, 3=w+x, 4=r, 5=r+x, 6=r+w, 7=r+w+x
- References: u=user, g=group, o=others, a=all

### List files

- `ls` list files in this directory
- `ls -ltr` list files in this directory with more details and in reverse chronological order
- `ls -ltra` same as above + list hidden files (names starting with `.`)
- `ls -ltr | grep "^l"` Lists all symlinks (`ls -ltr` lists symlinks with `l` as first character of output)

### Symlinks 

- Symbolic or soft links. Pointer to a file. 
- `ln -s /java/jdk7 jdk` create symlink jdk which points to `/java/jdk7`
- `ln -ns /java/jdk8 jdk` update symlink jdk to point to `/java/jdk8`


### Checking logs

- `tail -f logfile` output appended data as file grows (f=follow)
- `less +F logfile` open file, and output appended data as file grows

### Text manipulation

- `head file` display first 10 lines 
- `head -20 file` display first 20 lines 
- `tail file` display last 10 lines
- `tail -5 file` display last 5 lines
- `head -20 file | tail -1` display 20th line
- `cut -f3 file` display 3rd field for each line, tab as separator
- `cut -d',' -f3 file` display 3rd field for each line, `,` as separator
- `cut -c3-6 file` display characters from 3rd to 6th position for each line
- `cut -c7- file` display characters from 7th to end of each line

### Sed

- `sed s/unix/linux file` replace first occurrence of "unix with "linux"
- `sed s/unix/linux/3 file` replace 3rd occurrence
- `sed s/unix/linux/g file` replace all occurrences
- `sed s/unix/linux/3g file` replace all occurrences starting from 3rd one
- `sed -i '1 d' file` delete header of file
- `sed -i '$ d' file` delete footer of file
- `sed –n '10 p' file` print 10th line of the file 

### Networking

- `ping hostname` or `telnet hostname port` check if remote host is alive
- `scp /dir/file user@hostname:/targetdir/file` copy file to different host
- `netstat -a | grep "port"` check host connected to machine's port

### Space

- `df -h` space in current drive (`-h` is human readable format)
- `du -h .` sizes of all files in current directory
- `du -sh .` sizes of current directory
- `du /bin/* | sort -n` sort all files based on size (asc)


### Miscellaneous

- `lsof file` list processes using the file
- `rev file` reverses the text in each line
- `echo "string" | rev ` reverses the string
- `sort file` sorts file lines alphabetically 
- `sort -n file` sorts file lines numerically
- `uniq file` filter out adjacent duplicate lines and print
- `uniq -c file` print with count at the begining of each line of output
- `uniq -d file` print only duplicates