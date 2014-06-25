---
layout: post
title: "bash cheat sheet"
date: 2014-02-06 23:35:02 +0200
author: <a rel="author" href="https://plus.google.com/117525803180879614771/about">Horea Christian</a>
comments: true
categories: [Linux, Gentoo, bash, coding]
published: true
---

This is a collection of bash scripts solving a series of eclectic use cases which we have encountered in the past.
These instructions use linux commands and directory structures. 

<!-- more -->
## Replace Sting in All Files in Directory
Especially when coding you may find yourself changing a variable name or some library path, which is referenced in multiple places across multiple files.
[sed](https://en.wikipedia.org/wiki/Sed) and [grep](https://en.wikipedia.org/wiki/Grep) come in handy here, and can help you do all that menial name changing in one simple line from your terminal:

```bash
grep -rl . | xargs sed -i 's/text-you-want-to-replace/your-new-text/g'
``` 

Please note that the slashes (```/```) in the above code are part of the sed syntax and should stay the same independently of your text change.
Also note that [some characters need escaping in sed](http://unix.stackexchange.com/questions/32907/what-characters-do-i-need-to-escape-when-using-sed-in-a-sh-script).

## Check Sequence of Files for Missing Entries
Say you are keeping your photography files in a single directory and have them incrementally numerated.
And say you would like to check if there is any index number wherefore neither a ```.JPG``` nor a ```.NEF``` file is present.
The following script would help you find any such indices starting form ```DSC_a0000``` and up to ```DSC_a8888```:

```bash
for i in DSC_a{0000..8547}; do [[ ! -e "${i}.JPG" && ! -e "${i}.NEF" ]] && echo "No File with $i found"; done
```

This command can also be easily modified to suit slightly different needs - say you are only interested in indices for which ```.JPG``` files are missing:

```bash
for i in DSC_a{0000..8547}; do [[ ! -e "${i}.JPG" ]] && echo "No File with $i.JPG found"; done
```

Or specifically indices for which a ```.NEF``` file is present but a ```.JPG``` file is missing:

```bash
for i in DSC_a{0000..8547}; do [[ ! -e "${i}.JPG" && -e "${i}.NEF" ]] && echo "No File with $i.JPG found, but $i.NEF exists"; done
```

## Append Text Line to Text File

```bash
echo your text here, you may even add special characters: .-, \ \\ \" \; >> /your/file/path
```

Quotation marks are optional here and come in handy only if your code snippet contains many special characters (```;```, ```\```, etc.).
You can escape single characters by prefixing them with a backslash (```\```).


---
<sup>Browse the history of this file *or* find static versions to cite via [its GitHub page](https://github.com/TheChymera/chymeric_tutorials/blob/master/source/_posts/2014-02-06-bash-cheat-sheet.markdown)!</sup>
