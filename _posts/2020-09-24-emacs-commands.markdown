---
layout: post
title:  "Emacs commands"
date:   2020-09-24 16:39:24 +0200
categories: emacs
---

# How to guide:  

- Find emacs init file: [here][init] you can find an explanation. Run: C-x C-f ~/.emacs.d/init.el RET

To restart after some change has happenned run: M-x eval-buffer

[init]: https://www.emacswiki.org/emacs/InitFile

- Use org-mode: [here][org] you can find a manual and here a [quickstart][quick] guide.

[org]: https://orgmode.org/
[quick]: https://orgmode.org/quickstart.html

- Use org-journal: see [project page][journal]

[journal]: https://github.com/bastibe/org-journal

- Use latex in emacs: see [latex][latex]

[latex]: https://opensource.com/article/20/4/emacs-org-mode

- Use emacs commands: see the GNU Emacs [manual][gnu]

[gnu]: https://www.gnu.org/software/emacs/manual/html_node/emacs/index.html

# Concepts explanation

- Difference between frame, window, buffer and file.

[See here][diff]

[diff]: https://emacs.stackexchange.com/questions/13583/whats-the-difference-between-a-buffer-a-file-a-window-and-a-frame

# Help commands  

| Command  | Description                     |
| ---------| ------------------------------- |
| C-h ?    | help for help                   |
| C-h k    | documentation of a key sequence |

# Search commands  

| Command  | Description |
| ------------- | ------------- |
| C-s | interactive search (isearch) |
| C-s | in isearch, jump to next occurrence |
| C-r | in isearch, jump to previous occurrence |
| C-g | in isearch, exit place cursor at original position |
| Enter | in isearch, exit and place cursor at current position |



[A reference][searchref]

[searchref]: http://ergoemacs.org/emacs/emacs_search_current_word.html

# Fix mistakes  

| Command       | Description   |
| ------------- | ------------- |
| C-g           | quits current command |


# Buffer commands 

| Command       | Description                                                 |
| ------------- | ----------------------------------------------------------- |
| C-x o         | moves to "other" buffer                                     |
| C-x k         | kills specified buffer                                      |
| C-x LEFT      | select previous buffer in the buffer list (previous-buffer) | 
| C-x RIGHT     | select the next buffer in the buffer list (next-buffer)     |

# Window commands

| Command       | Description                                                                                    |
| ------------- | ---------------------------------------------------------------------------------------------- |
| C-x 0         | Delete the selected window                                                                     |
| C-x 2         | Split the selected window into two windows, one above the other (split-window-vertically)      |
| C-x 3         | Split the selected window into two windows positioned side by side (split-window-horizontally) | 

# Coq commands  

See settings in .emacs configuration file.

| Command       | Description |
| ------------- | ------------- |
| C-c C-d       | see definition of Coq code |

# Latex commands

| Command       | Description |
| ------------- | ------------- |
| C-c C-x C-l   | see preview of latex snippets |

# Terminal commands

| Command       | Description |
| ------------- | ------------- |
| M-x term   | launch terminal |
