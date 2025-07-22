---
layout: post
title: Missing Semester 2 - Working through some shell scripting poblems
date: 2025-01-12
categories: shell
---

Continuing with the 2nd [MIT Missing][mit-missing] Semester exerises. Follow along with this part [here.][this-part]

1. Read `man ls` and write an `ls` command that lists files in the following manner:
   - Includes all files, including hidden files
   - Sizes are listed in human-readable format (e.g. 454M instead of 454279954)
   - Files are ordered by recency
   - Output is colorized

   Reading `man ls`, I created the following script for this:

   ```sh
   lse (){
      ls -aGtlh
   }
   ```

   Here:
   - `-a` includes hidden files.
   - `-G` enables a colourized output.
   - `-t` sorts files by recency.
   - `-l` enables long format.
   - `-h` puts file sizes in human-readable format.

2. The main difficulty this problem is decyphering the syntax required for conditinal statements and command substitutions.

   ```sh
    # Store the saved directory path as a hidden file, note we don't use spaces around the equals sign when shell scripting.
   MARCO=~/.marco_polo_path

   # save current directory to MARCO and tell user what happened.
   marco() {
      pwd > "$MARCO"
      echo "Saved current directory: $(pwd)"
   }
   ```

   For the next part I used
   [this page](https://zsh.sourceforge.io/Doc/Release/Conditional-Expressions.html) of the zsh documentation to determine how to flag the if statements. The `-f` flag checks if the `$MARCO` **f**ile exists whereas the `-d` flag checks if the `$target_dir` **d**irectory exists.

   ```sh
   # go to saved directory
   polo() {
     if [ -f "$MARCO" ]; then
         # <"$MARCO_FILE" is shorthand for reading the contents of $MARCO. This is known as a command substitution.
         target_dir=$(<"$MARCO")
         if [ -d "$target_dir" ]; then
             cd "$target_dir" || echo "Failed to navigate to $target_dir"
         else
             echo "Saved directory no longer exists: $target_dir"
         fi
     else
         echo "No directory saved. Use 'marco' to save one first."
     fi
   }
   ```

3. Next, we write a shell script that repeatedly runs the following until it fails and logs our outputs to a file as it runs.

   ```sh
   #!/bin/zsh

   n=$(( RANDOM % 100 ))

   if [[ n -eq 42 ]]; then
       echo "Something went wrong"
       >&2 echo "The error was using magic numbers"
       exit 1
   fi

   echo "Everything went according to plan"
   ```

   So we have a 1 in 100 chance of a failure. `>&2` means that our second message is directed (`>`) to a file descriptor (`&`) described by (`2`). Here:
   - `STDOUT`, `1` represents the Standard Output so the place where our output generally is sent.
   - `STDERR`, `2` represents the Standard Error so the place where we output error codes to. Not the standard error in statistics.
   - `>&2` is equivalent to `1>&2` where `1` represents the standard output `STDOUT`. Therefore, `STDOUT` is being redirected to `STDERR`. This can be used before after or between `echo` and the string in question.

   ```sh
   #!/bin/zsh
   file=$1
   max=$2
   # setup logfile
   logfile="${file%.*}.log" # set log filename based on input file
   "./$file" > $logfile
   count=1
   exit_code=0
   # run $file outputting to both the standard output (stdout) and standard error (stderror) to $logfile
   while [[ count -lt max && $exit_code -eq 0 ]];
       do
           #redirect STDERR to STDOUT
           "./$file" >> $logfile 2>&1
           # ?! is 0 by default. Above it is specified as 1 when n = 42 via exit 1
           exit_code=$?
           cat $logfile
           # read last line of the logfile and print
           if [[ $exit_code -ne 0 ]];
           then
               break
           fi
           # increment our count by 1
           (( count += 1 ))
   done
   if [[ $exit_code -ne 0 ]];
   then
       # piping into tee -a (append) means we also append this echo to our logfile
       echo "Failure after $count successful runs. See log at /tmp/$logfile" | tee -a $logfile
   fi
   if [[ $count -eq $max && $exit_code -eq 0 ]];
   then
       echo "No fails after $count runs. See log at /tmp/$logfile" | tee -a $logfile
   fi
   ```

4. Your task is to write a command that recursively finds all HTML files in the folder and makes a zip with them. Note that your command should work even if the files have spaces (hint: check -d flag for xargs).

   I created the following directory setup:

   ```console
   .
   ├── html
   ├── test a.html
   ├── test1.html
   └── tests2
       ├── hello.html
       ├── test html
       ├── test2.html
       └── tests3
           ├── goodbye.html
           ├── test b.html
           ├── test.py
           └── test3.html

   3 directories, 10 files
   ```

   To show this directory tree yourself use `tree` from within your project directory. `tree` can be installed via `brew install tree` (macOS) or using `sudo apt-get install tree` (Linux). Be careful using sudo when installing software though.

   I used the following to compress all the Html files here into a `compressed.zip` file:

   ```sh
   #!/bin/zsh
   find . -path '*.html' -type f -print0 | xargs -0 zip -rj compressed
   ```

   There are a lot of arguments to unpack here - we'll start with before the first pipe (`|`). The `find` function is used to recursively search through the file tree, with the first argument, `.` specifying that we want to start our search in the current directory. `-path` allows us to specify a pattern we wish to match throughout this search - in this case files ending in `.html`. `-type f` is only true if files are regular files. We use the combination of `-print0` and `-0` to make `find` work effectively with `xargs`.

   From thrre, `xargs` reading the strings from `find` as a standard input (the `html` files recursively found within the current directory tree). Here `zip` means we are compressing this standard input into a zip file. `-r` standards for recusively here meaning that we will travel through the files recursively, whilst `-j` junks the paths leaving them out of the compressed zip file, which here we call `compressed`.

5. Write a command or script to recursively find the most recently modified file in a directory. More generally, can you list all files by recency?

   In this one we can simplify the find expression from the previous exercise to start with. `ls -t` lists our files by recency and if we give `rec` a number as an argument it will only read out that number of rows due to `head -n`.

   ```sh
   rec (){
      if [[ $1 ]]; then
         find . -type f -print0 | xargs -0 ls -t | head -n "$1"
      else
         find . -type f -print0 | xargs -0 ls -t
      fi
   }
   ```

[mit-missing]: https://missing.csail.mit.edu/
[this-part]: https://missing.csail.mit.edu/2020/shell-tools/
