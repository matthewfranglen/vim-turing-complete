What minimum set of actions make Vim turing complete?
=====================================================

If you take every action that Vim provides then it is possible to create a
turing complete sequence of actions. This is because both vimscript and the
shell are turing complete.

It is possible to do a great deal with a relatively small number of actions.
For example:

You can call a macro whilst running it
--------------------------------------

```vimscript
Ihello world!@a
```
