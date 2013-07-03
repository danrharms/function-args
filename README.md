# Introduction

This package extends `c++-mode` completion provided by [CEDET][cedet] for [Emacs][emacs].

[cedet]: http://cedet.sourceforge.net/intellisense.shtml
[emacs]: http://www.gnu.org/software/emacs/

# Installation

Clone this repository:

    $ cd ~/.emacs.d/
    $ git clone https://github.com/abo-abo/function-args

Add to `.emacs`:

    (add-to-list 'load-path "~/.emacs.d/function-args")
    (require 'function-args)

Also, make sure that you have CEDET installed (it's part of Emacs since 23.2, so you probably do).

# Additional setup

Put c++-mode as default for *.h files (improves parsing):

    (add-to-list 'auto-mode-alist '("\\.h\\'" . c++-mode))

Enable case-insensitive searching:

    (set-default 'semantic-case-fold t)
    
If your includes aren't located in default dirs e.g. /usr/include/ etc, then you have to do something like this:

    (semantic-add-system-include "~/Software/deal.II/include/" 'c++-mode)

# Main functions

### `fa-show`

Show an overlay hint with current function arguments like so:

![screenshot](https://raw.github.com/abo-abo/function-args/master/doc/screenshot-1.png)

The point position is tracked and the current hint argument is updated accordingly.
After you've called it with `M-i`, you can cycle the overloaded functions with `M-n`/`M-h`.
You can dismiss the hint with `M-u` or by editing anywhere outside the function arguments.

### `fa-jump`

While the overlay hint is active, jump to the current function.
The default shortcut is `M-j`.
If the overlay isn't active,
call whatever was bound to `M-j` before (usually it's `c-indent-new-comment-line`).

### `moo-complete`

It's essentially a c++-specific version 'semantic-ia-complete-symbol.
It behaves better, because it accounts more for function overloading and inheritance.
You can invoke it with `M-o` by default.

# Bugs

### Reporting

If you wish to report a bug, please try to reproduce it first
with the newest Emacs like so:

    $ emacs -q -l ./function-args.el ~/test.cc

### bzr CEDET

The latest version of [CEDET][bzr] can sometimes give more completion candidates.
I recommend to install it if you're having problems with the CEDET that comes with Emacs.

[bzr]: http://cedet.sourceforge.net/bzr-repo.shtml

### Semantic refresh

If you're getting a completion only sometimes under the same conditions,
try `M-x RET semantic-force-refresh`.



