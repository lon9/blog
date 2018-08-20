+++
categories = [
  "Programming",
]
date = "2015-10-10T22:16:32+09:00"
description = "The way to push submodules together with main modules with ShellScript."
tags = [
  "Git",
  "Github",
  "ShellScript"
]
title = "Push submodules together with main module"

+++

This blog is controlled as submodule of `hugo`, CMS written with Golang, on Github.  So I want to push this blog with main CMS module, when I write a post and build blog templates.   
Then I wrote a ShellScript to do this. 

```sh
#!/bin/sh

# For pushing to Github

CMDNAME=`basename $0`
MSG="Content updated"
USAGE="Usage :$CMDNAME [-m <commit-message>]"


while :
do
  case $1 in
    -m) shift
      if [ "$1" = "" ]; then
        echo "$USAGE" 1>&2
        exit 1
      else
        MSG=$1
      fi
      break
      ;;
    --)shift
      break
      ;;
    -*) echo "$USAGE" 1>&2
      exit 1
      ;;
    *) break
      ;;
  esac
done

echo "Commit submodules..."
git submodule foreach git add -A
git submodule foreach git commit -m "$MSG"

echo "Commit main module..."
git add -A
git commit -m "$MSG"

echo "Push all"
git submodule foreach git push -u origin master
git push -u origin master
```

`-m` option allow you to add commit message like this.   

`./push -m "First commit"`   

This will write same message for sub and main modules.
