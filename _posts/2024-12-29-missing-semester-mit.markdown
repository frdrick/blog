---
layout: post
title: Filling in some gaps when using the shell
date: 2024-12-29
categories: shell
---

Recently I have been trying to fill in the gaps in my fundamental computer science skills. I did not study computer science formally at university so find there are small gaps in my knowledge that can hold me back on data science projects.

Luckily, there are incredible resources available for free that really help with learning these techniques.

First, see Harvard's excellent cs50 course [here][cs50].

Second, and the subject of this post, is MIT's _The Missing Semester of Your CS Education_ (found [here][mit-missing]). Since I didn't study CS I imagine there are quite a few more missing semesters than this alone for me, but some of the elements of this course seem extremely useful to me so far. Primarily because of the amount of time spent on preprocessing when using real data.

## Missing Semester Exercises

Follow along with this part of the course [here](https://missing.csail.mit.edu/2020/course-shell/).

1. Create a new directory called `missing` under `/tmp`.

```console
$ cd /tmp
$ mkdir missing
```

2. Look up the `touch` program using `man`.

```console
$ man touch
```

3. Use `touch` to create a new file called `semester` in `missing`.

```console
$ cd /missing
$ touch semester
```

4. Write the following into that file, one line at a time:

```
#!/bin/sh
curl --head --silent https://missing.csail.mit.edu
```

We can accomplish this using `echo`, `>` and `>>`.

```console
set the first line of semester to #!bin/sh
$ echo "#!bin/sh" > semester
# append the next line to semester. `>>` appends rather than overwriting.
$ echo "curl --head --silent https://missing.csail.mit.edu" >> semester
```

5. Try to execute `semester` using `./semester`
   `./semester` returns:

```console
zsh: permission denied: ./semester
```

6. We can solve this via

```zsh
$ sh ./semester
```

Which gives:

```output
HTTP/2 200
server: GitHub.com
content-type: text/html; charset=utf-8
last-modified: Sat, 21 Dec 2024 16:53:01 GMT
access-control-allow-origin: *
etag: "6766f26d-205d"
expires: Sun, 29 Dec 2024 14:18:57 GMT
cache-control: max-age=600
x-proxy-cache: MISS
x-github-request-id: E182:12E922:803EEE6:8138ED3:677157F9
accept-ranges: bytes
age: 0
date: Sun, 29 Dec 2024 14:23:57 GMT
via: 1.1 varnish
x-served-by: cache-par-lfpg1960069-PAR
x-cache: HIT
x-cache-hits: 0
x-timer: S1735482237.092437,VS0,VE110
vary: Accept-Encoding
x-fastly-request-id: 1f41026f12a33ce0f4a66138fcfb5032689171b8
content-length: 8285
```

6. In macOS we can use `pbcopy` and `pbpaste` to copy or paste outputs from the terminal into the clipboard. For instance, to copy the above text I used:

```console
$ sh ./semester | pbcopy
```

[This medium article](https://medium.com/@codenameyau/how-to-copy-and-paste-in-terminal-c88098b5840d) shows that in linux this can be easily replicated. These are aliases (names given to commands so they can be used quickly and easily):

```console
Linux version of OSX pbcopy and pbpaste.
$ alias pbcopy='xsel — clipboard — input'
$ alias pbpaste='xsel — clipboard — output'
```

7. We see why `./semester` doesn't work using:

```console
Using -l gives a longer form output from the ls command.
$ ls -l
```

This should give something like:

```console
total 8
-rw-r--r--@ 1 <your-username>  wheel  63 29 Dec 13:00 semester
```

8. Looking up the `chmod` program.
   The start of this output (`-rw-r--r--`) is well described in the [chmod wikipedia article](https://en.wikipedia.org/wiki/Chmod). The nine characters **after the first hyphen** describe the permissions of the `semester` file. In each group of 3 letters, **r**, **w** and **x** describe the **r**ead, **w**rite and e**x**ecute permissions. We can also use:

```console
$ man chmod
```

This opens a vi window, which can be quite intimidating initially. This can be scrolled through using the arrow keys or vi motions (`j` for down, `k` for up, `l` for right, `h` for left). Most useful are the `?` and `/` commands which allow for searching forwards or backwards for a word. The window can be quit using `q`. When I was in the `chmod` manual, I used `/mode` to search for occurences of the word `mode`. Often `/example` can also be really useful.

9. Using `chmod` to make `./semester` run without prepending with `sh`.

```console
$ chmod u+x semester
```

This will, for the current user, add execute permissions for semester.

10. Run semester and write the last-modified date output to a file called `last-modified.txt` in the home directory.

```console
./semester | grep last-modified > ~/last-modified.txt
```

- We pipe into the ouput of `./semester` with `|`.
- `grep` searches for the string last-modified.
- Output this result into the next file using `>`.
- Specify the home directory my prepending our filename with `~/`.

[cs50]: [https://cs50.harvard.edu/x/2024/]
[mit-missing]: [https://missing.csail.mit.edu/]
