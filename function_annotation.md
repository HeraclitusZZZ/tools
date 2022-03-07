# Function Annotation

Function annotations are arbitrary python expressions that are associated with various part of functions. These expressions are evaluated at compile time and have no life in python’s runtime environment. Python does not attach any meaning to these annotations. They take life when interpreted by third party libraries, for example, mypy.

## Purpose of function annotations

The benefits from function annotations can only be reaped via third party libraries. The type of benefits depends upon the type of the library, for example

1. Python supports dynamic typing and hence no module is provided for type checking. Annotations like

```console
[def foo(a:”int”, b:”float”=5.0)  -> ”int”]
```

(syntax described in detail in the next section) can be used to collect information about the type of the parameters and the return type of the function to keep track of the type change occurring in the function. ‘mypy’ is one such library.

2. String based annotations can be used by the libraries to provide better help messages at compile time regarding the functionalities of various methods, classes and modules.

## Syntax of function annotations

They are like the optional parameters that follow the parameter name.

Note: The word ‘expression’ mentioned below can be the type of the parameters that should be passed or comment or any arbitrary string that can be made use by external libraries in a meaningful way.

1. **Annotations for simple parameters** : The argument name is followed by ‘:’ which is then followed by the expression. Annotation syntax is shown below.

```python
def foobar(a: expression, b: expression = 5):
```

2. **Annotations for excess parameters** : Excess parameters for e.g. *args and **kwargs, allow arbitrary number of arguments to be passed in a function call. Annotation syntax of such parameters is shown below.

```python
def foobar(*args: expression, *kwargs: expression):
```

3. **Annotations for nested parameters** : Nested parameters are useful feature of python 2x where a tuple is passed in a function call and automatic unpacking takes place. This feature is removed in python 3x and manual unpacking should be done. Annotation is done after the variable and not after the tuple as shown below.

```python
def foobar((a: expression, b: expression), (c: expression, d: expression)):
```

4. **Annotations for return type** : Annotating return type is slightly different from annotating function arguments. The ‘->’ is followed by expression which is further followed by ‘:’. Annotation syntax of return type is shown below.

```python
def foobar(a: expression)->expression:
```

## Grammar

```console
decorator    :  ‘@’ name_  [‘(’ [arglist] ‘)’] NEWLINE
decorators   :  decorator+
funcdef      :  [decorators] ‘def’ NAME parameters [‘->’] ‘:’ suite
parameters   :  ‘(’ [typedarglist] ‘)’
typedarglist :  (( tfpdef [‘=’ test] ‘, ’)* (‘*’ [tname]
(‘, ’ tname [‘=’ test])* [‘, ’ ‘ **’ tname] | ‘**’ tname)
| tfpdef [‘=’ test (‘, ’ tfpdef [‘=’ test])* [‘, ’]])
tname        :  NAME [‘:’ test]
tfpdef       :  tname | ‘(’ tfplist ‘)’
tfplist      :  tfpdef (‘, ’ tfpdef)* [‘, ’]
```

```python
# Python program to print Fibonacci series
def fib(n:'int', output:'list'=[])-> 'list':
	if n == 0:
		return output
	else:
		if len(output)< 2:
			output.append(1)
			fib(n-1, output)
		else:
			last = output[-1]
			second_last = output[-2]
			output.append(last + second_last)
			fib(n-1, output)
		return output
print(fib(5))
```

## Reference

[1] https://www.geeksforgeeks.org/function-annotations-python/
