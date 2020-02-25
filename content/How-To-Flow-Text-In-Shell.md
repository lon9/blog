---
categories: [
  "Programming"
]
date: "2015-11-19T01:28:32+09:00"
description: "ShellScript for flowing text in the shell"
tags: [
  "ShellScript"
]
title: "How To Flow Text In Shell"
---

[![https://gyazo.com/7dda31251c37e8fd41439324b423160d](https://i.gyazo.com/7dda31251c37e8fd41439324b423160d.gif)](https://gyazo.com/7dda31251c37e8fd41439324b423160d)

This snippet flows some text in your shell.  It use in the last of presentation or something.

```bash
#!/bin/bash

CMD_NAME=`basename $0`
SPACE=`tput cols`
FILE_NAME=

if [ $# -ne 1 ]; then
  echo "USAGE: $CMD_NAME file_name"
  exit 1
fi

# Trapping signals
trap 'tput smam; exit 1' 1 2 3 15

FILE_NAME=$1

while [ $SPACE -gt 0 ];
do
  while IFS='' read LINE
  do
    [[ $SPACE > 0 ]] && printf "%${SPACE}s" ' '
    tput rmam; printf "%s\n" "$LINE"
  done < $FILE_NAME
  SPACE=$(( SPACE - 1 ))
  sleep 0.02
  if [ $SPACE -gt 0 ]; then
    clear
  fi
done

tput smam
```

And then type `./flow_text <text-file>`
