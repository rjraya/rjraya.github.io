---
layout: post
title:  "Emacs commands"
date:   2020-09-24 16:39:24 +0200
categories: emacs
---

## Where is the emacs init file?  

[Here][init] you can find an explanation. To be quick run:

 C-x C-f ~/.emacs.d/init.el RET

 To restart after some change has happenned run:
 
  M-x eval-buffer

## How do I learn org-mode?  

[Here][org] you can find a manual and a [quickstart][quick] guide.

## How do I use org-journal?

See [project page][journal]

## How do I use latex in emacs?

See: [latex][latex]

## How do I learn emacs commands?  

The GNU Emacs [manual][gnu].

# Difference between frame, window, buffer and file.

[See here][diff]

[diff][https://emacs.stackexchange.com/questions/13583/whats-the-difference-between-a-buffer-a-file-a-window-and-a-frame]

# Help commands  

See: https://www.cs.colostate.edu/helpdocs/emacs.html

| Command  | Description                     |
| ---------| ------------------------------- |
| C-h ?    | help for help                   |
| C-h k    | documentation of a key sequence |

# Search commands  

| Command  | Description |
| ------------- | ------------- |
| C-s |  prompts for text string and then searches from the current cursor position forwards in the buffer  |

# Fix mistakes  

| Command       | Description   |
| ------------- | ------------- |
| C-g           | quits current command |


# Buffer commands 

| Command       | Description   |
| ------------- | ------------- |
| C-x o         | moves to "other" buffer |
| C-x k         | kills specified buffer |

# Window commands

| Command       | Description   |
| ------------- | ------------- |
| C-x 0         | Delete the selected window  |

# Coq commands  

See settings in .emacs configuration file.

| Command       | Description |
| ------------- | ------------- |
| C-c C-d       | see definition of Coq code |

# Latex commands

| Command       | Description |
| ------------- | ------------- |
| C-c C-x C-l   | see preview of latex snippets |

[init]: https://www.emacswiki.org/emacs/InitFile
[quick]: https://orgmode.org/quickstart.html
[org]: https://orgmode.org/
[gnu]: https://www.gnu.org/software/emacs/manual/html_node/emacs/index.html
[journal]: https://github.com/bastibe/org-journal
[latex]: https://opensource.com/article/20/4/emacs-org-mode