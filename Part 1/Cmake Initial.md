create a file named `hello.txt` with the following content
`message("Hello world!")`

In cmd run `cmake -P hello.txt`. (The `-P` option runs the given script, but doesn’t generate a build pipeline.) As expected, it prints `Hello world!`

##### **All Variables Are Strings**

You can substitute a variable inside a string literal by surrounding it with `${}` called a **variable reference**

`message("Hello ${NAME}!")`

Now, if we define `NAME` on the `cmake` command line using the `-D` option, the script will use it:

`$ cmake -DNAME=Newman -P hello.txt`
`Hello Newman!`

-DNAME --> Varibale name

##### **Define a variable inside a script**

`set(THING "funk")`
`message("We want the ${THING}!")`

##### **FLow Control**

**If**

```
if(WIN32)
    message("You're running CMake on Windows.")
endif()
```

**While**
`set(A "1")`
`set(B "1")`
`while(A LESS "1000000")`
    `message("${A}")                 # Print A`
    `math(EXPR T "${A} + ${B}")      # Add the numeric values of A and B; store result in T`
    `set(A "${B}")                   # Assign the value of B to A`
    `set(B "${T}")                   # Assign the value of T to B`
`endwhile()`

