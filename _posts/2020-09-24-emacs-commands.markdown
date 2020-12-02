---
layout: post
title:  "Emacs commands"
date:   2020-09-24 16:39:24 +0200
categories: emacs
---

# Where the hell is the emacs init file?

[Here][init] you can find an explanation. To be quick run:

C-x C-f ~/.emacs.d/init.el RET

# How do hell do I learn org-mode?

[Here][org] you can find a manual and a [quickstart][quick] guide.

# Help commands

See: https://www.cs.colostate.edu/helpdocs/emacs.html

| Command  | Description |
| ------------- | ------------- |
| C-h ? | help for help  |

# Search commands

| Command  | Description |
| ------------- | ------------- |
| C-s |  prompts for text string and then searches from the current cursor position forwards in the buffer  |

TODO: once found, how to scan new commands

# Fix mistakes

| Command       | Description   |
| ------------- | ------------- |
| C-g           | quits current command |


* 	C-g 	keyboard-quit: if while typing a command you make a mistake and want to stop,
  this aborts a command in progress

# Coq commands

TODO: is it my settings?

| Command  | Description |
| ------------- | ------------- |
| C-c C-d | see definition of Coq code |

[init]: https://www.emacswiki.org/emacs/InitFile
[quick]: https://orgmode.org/quickstart.html
