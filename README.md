# Smart-Dash

Smart-Dash mode is an Emacs minor mode which redefines the dash key to
insert an underscore within C-style identifiers and a dash otherwise.

The goal is to allow you to type the `underscore_separated_identifiers` that are
common in C, Python or PHP as comfortably as you would type
`lisp-style-identifiers`.

## Downloading

Smart-Dash mode is maintained under Git on github.com.
    Get it by running
```
      git clone https://github.com/malsyned/smart-dash
```

## Installing

Add the folder where you've unpacked smart-dash to your Emacs
    load-path, then `(require 'smart-dash)`

## Usage

Activate the Smart-Dash minor mode in a buffer with `M-x
smart-dash-mode` or by adding `smart-dash-mode` to
the load hook for your favorite programming language's major mode.

Now, just type your code like you normally would, but stop pressing
the shift key when you need an underscore inside an identifier.

If you need to type a literal dash right after an identifier (say, to
type a cramped arithmetic expression like `x-3`), use the emacs
quoted-insert character `C-q` to inhibit Smart-Dash behavior for one
character, or use the minus key on the number pad.

## Will It Get in My Way?

TL;DR: no, not if you put spaces around "`-`" used for subtraction.

In creating Smart-Dash I've tried to make sure that it doesn't get in your way.
For example, Smart-Dash uses the syntax information provided by the current mode to always insert a dash inside strings and comments, and has
special cases for common idioms in C-like modes ([described
below](#additional-features-for-c-like-modes)).

However, since its behavior is heuristic, it may not interact well with your
particular coding style.  If you are in the habit of putting spaces between your
identifiers and your arithmetic operators as in "`foo - 7`" then you'll probably
get along with Smart-Dash just fine.  If, however, you frequently write
close expressions like "`x-3`", Smart-Dash might not be the right fit for
you.

## Additional Features for C-Like Modes

C has two situations where almost all developers and style guides put
a dash directly after an identifier.  They are the `->` struct access
operator and the postfix `--` post-decrement operator.  When
Smart-Dash mode is activated in a C-like mode that use these
operators, Smart-Dash activates two workarounds.

The first is that if you type `>` after an underscore, the underscore will be
replaced with a dash.  The typical sequence of operations, then, looks like
this:

![Smart-Dash C struct access](media/smart-dash-c-struct.gif "foo
foo_
foo->
foo->bar")

The second is a little more complicated, but I've found that it works in all
syntactically-valid scenarios.  If you type a dash and the previous character is
an underscore, both characters are replaced by dashes.  That sequence looks like
this:

![Smart-Dash C postfix decrement](media/smart-dash-c-postfix-dec.gif "foo
foo_
foo--")

This requires that if you want a double-underscore in your identifier in a
C-like mode, you will have to type it yourself. As for the rare case where you
want to type `__foo__--`, Smart-Dash attempts to detect and handle it.  It
looks like this:

![Smart-Dash C postfix decrement after underscore](media/smart-dash-c-dunder-dec.gif "__foo
__foo_
__foo--
__foo_--
__foo__--")

By default, these workarounds are activated for C, C++, and Objective C. This list is [customizable](#customizing).

## Customizing

You can customize the behavior of Smart-Dash mode by typing `M-x
customize-group RET smart-dash RET`.
