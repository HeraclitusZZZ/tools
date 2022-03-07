# Assert

## Assertion

Assertions are statements that assert or state a fact confidently in your program. For example, while writing a division function, you're confident the divisor shouldn't be zero, you assert divisor is not equal to zero.

Assertions are simply boolean expressions that check if the conditions return true or not. If it is true, the program does nothing and moves to the next line of code. However, if it's false, the program stops and throws an error.

It is also a debugging tool as it halts the program as soon as an error occurs and displays it.

## Python Assert Statement

Python has built-in `assert` statement to use assertion condition in the program. `assert` statement has a condition or expression which is supposed to be always true. If the condition is false assert halts the program and gives an `AssertionError`.

Syntax for using Assert in Pyhton:

```console
assert <condition>
```

```console
assert <condition>,<error message>
```

In Python we can use `assert` statement in two ways as mentioned above.

1. `assert` statement has a condition and if the condition is not satisfied the program will stop and give `AssertionError`.
2. `assert` statement can also have a condition and a optional error message. If the condition is not satisfied assert stops the program and gives `AssertionError` along with the error message.

## Reference

[1] https://www.programiz.com/python-programming/assert-statement
