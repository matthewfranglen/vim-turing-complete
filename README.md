What minimum set of actions make Vim turing complete?
=====================================================

If you take every action that Vim provides then it is possible to create a
turing complete sequence of actions. This is because both vimscript and the
shell are turing complete.

Capabilities
------------

It is possible to do a great deal with a relatively small number of actions.
For example:

### You can call a complex repeat whilst running it

This script needs to be yanked into the `a` register. You can do this with `0"ay$`.

```vimscript
Ihello world!@a
```

When executed (`@a`) this will endlessly repeat _hello world!_.
This is because it inserts that text and then calls itself again.

This allows recursion.

### You can create a complex repeat while running a complex repeat

This script needs to be yanked into the `a` register. You can do this with `0"ay$`.

```vimscript
oIhello world!0"by$dd@b@a
```

When executed (`@a`) this will endlessly repeat _hello world!_.
This is because it populates the `b` register with `Ihello world!` and then calls it.

This uses `<ESC>` after calling `@b` to demonstrate that the complex repeat invocation
remains in insert mode after leaving the `b` complex repeat. It would be possible to end
insert mode within the `b` complex repeat by ending it with `<C-V><C-V><C-V><ESC>`.

With careful construction conditional complex repeat invocation can be achieved.
This can be done by reducing and mapping a block of text into a complex repeat
using actions such as `:g`, `:v` and `:s`.

### You can use the current buffer as a working memory

This script needs to be yanked into the `a` register. You can do this with `0"ay$`.

```vimscript
@a
```

You need to execute this while the cursor sits on or before a number.
When executed (`@a`) this will endlessly increment the number.

By using `<C-A>` the current buffer has become readable as well as writeable.
This functionality has already been demonstrated by the other examples.
This just makes it explicit.

There are other ways to do this which permit greater power (e.g. multi-repeat).

Turing Completeness
-------------------

### Turing Machines

The definition of a turing machine is available [here](http://plato.stanford.edu/entries/turing-machine/#Definition).

The turing machine requires the following:

 * An internal state
 * An infinite tape of symbols
 * A map of state and symbol to next state and action

It is perfectly possible to use buffers to represent all of these.
It's also convenient to have a fourth buffer to work over.

### Turing Completeness

A simple list of requirements is available [here](http://programmers.stackexchange.com/a/132420).

The turing complete language requires the following:

 * A way to perform conditional repetition
 * A way to read and write some form of storage
