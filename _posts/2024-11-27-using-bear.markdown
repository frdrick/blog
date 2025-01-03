---
layout: post
title:  "A year learning the command line interface"
date:   2024-11-27 09:53:01 +0000
categories: jekyll update
---
I have picked up a few really useful tricks in the command line interface over the past year of programming but have a hard time remembering them all. 
I have been using the sidebar in MacOS as a reference to newly learnt ones (recently switching to the [bear](https://bear.app/) note taking app). However now I feel like I should make a note of all the ones I keep forgetting here in the hope I will remember them better. 

<!-- ### Find and replace in vim/neovim -->
<!-- `:s/<search_term>/<replace_term>/g` -->
<!-- * `:%s` = full file; -->
<!-- End tags: -->
<!-- * `g` = **g**lobal -->
<!-- * `c` = **c**onfirm -->
<!-- * `i` = case **i**nsensitive -->
<!-- * `I` = case ~~i~~sensitive -->

### Copy current working directory to clipboard

To use this the following into the CLI:
`alias cpwd="pwd | tr -d '\n' | pbcopy && echo 'pwd copied to clipboard'"`

This came from [ Kyle Shevlin ](https://kyleshevlin.com/bash-shortcut-copy-your-present-working-directory-to-your-clipboard/)

### Fuzzy finder useful commands
*  `fzf`  [find on github](https://github.com/junegunn/fzf) immensely helpful for navigating the command line interface.
* Search current directory:
{% highlight console %}
ctrl+t
{% endhighlight %}
* Search previous CLI commands: 
{% highlight console %}
ctrl+r
{% endhighlight %}

### Navigating the line itself
Spending time moving around the line after a typo can be a pain. The following have saved me quite a bit of time:
* Go to the start of the command prompt (if in bash this is where the $ sign is)
{% highlight console %}
ctrl + a
{% endhighlight %}
* Go to the end:
{% highlight console %}
ctrl + e
{% endhighlight %}
* Toggle between the start of the line and the current position:
{% highlight console %}
ctrl + e
{% endhighlight %}
