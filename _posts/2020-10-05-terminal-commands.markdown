---
layout: post
title:  "Terminal utilities"
date:   2020-10-05 16:39:24 +0200
categories: bash
---

# Bash

[Wikipedia][wiki]
[Manual][man]

How to find the right bash command from documentation?

# Specific commands

| Command  | Description                   | References                  |
| -------- | ----------------------------- | --------------------------- |
| scp      | Copy files between computers  | [unix stack exchange][unix] |
| grep     | Search for pattern in files   |                             |


# Example use

| What | How |
|------|-----|
| Find text in files | grep -rnw '/path/to/somewhere/' -e 'pattern' |
| Find files with given name | find /path/to/file/ -iname filename* |



[wiki]: https://en.wikipedia.org/wiki/Bash_(Unix_shell)
[man]: https://www.gnu.org/software/bash/
[unix]: https://unix.stackexchange.com/questions/188285/how-to-copy-a-file-from-a-remote-server-to-a-local-machine
