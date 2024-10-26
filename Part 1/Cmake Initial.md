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

