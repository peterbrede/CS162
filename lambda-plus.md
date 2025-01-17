# Getting started with λ<sup>+</sup>

In this course, you will need two important tools: the manual, and the reference
interpreter (called `lamp`, short for "lambda plus"). Both can be downloaded
from Gauchospace and will be updated regularly, so make sure you have the latest
versions when you are doing the homeworks.

## Using `lamp`

The `lamp` binary provided on Gauchospace is compiled for Linux. This means that
you will either need to 1) run it on CSIL; or 2) run it from your own Linux
installation. Make sure to run `chmod +x` on `lamp` the first time you use it,
or else you may get a `Permission denied` error. Please let the TA know if you
have you have any questions about `lamp`.

### REPL

Once you have downloaded it on to your Linux machine of choice, you can execute
`lamp` directly to start a REPL (read-eval-print-loop). 

```plain
[bryantan@csilvm-02 demo]$ ls
lamp
[bryantan@csilvm-02 demo]$ ./lamp
Welcome to lambda+!
> 

```

You can then type in an expression and hit <kbd>Enter</kbd> to evaluate it:

```plain
> 1 + 2 * 3
<== 1 + (2 * 3)
==> 7
```

The `<==` line will show the expression that `lamp` will actually evaluate, while the
`==>` line shows the final value obtained by evaluating the expression. The former is
quite useful when you are using syntax sugar like the `fun` syntax:

```plain
> fun add_five with n = n + 5 in add_five 3
<== let add_five = lambda n. n + 5 in add_five 3
==> 8
```

`lamp` will also show a program trace when a runtime error occurs. This is to
make it easier to debug your programs and interpreter implementations:

```plain
> let x = !1 in 2 @ x
<== let x = !1 in 2 @ x
error: Cannot take head of non-cons value
in expression !1
in expression let x = !1 in 2 @ x
```

Here, we are attempting to take the head of an integer, but this is not allowed
because head is only defined for cons cells.

Lastly, you can quit out of the interpreter by hitting <kbd>Ctrl</kbd><kbd>c</kbd>.

### Program file mode

`lamp` can also be used to execute an expression contained within a file. To do this, provide a file name as an argument to `lamp`, and it will evaluate and print out the expression in the file. The file must contain exactly one expression. For example:

```plain
[bryantan@csilvm-02 demo]$ cat demo.lp
fun add_five with n =
  n + 5
in
add_five 3
[bryantan@csilvm-02 demo]$ ./lamp demo.lp
8

```
