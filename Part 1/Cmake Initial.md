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


##### **Lists**

```
set(ARGS "EXPR;T;1 + 1")
math(${ARGS})                                   # Equivalent to calling math(EXPR T "1 + 1")
```

```
set(ARGS "EXPR;T;1 + 1")
message("${ARGS}")                              # Prints: EXPR;T;1 + 1
```

```
set(MY_LIST These are separate arguments)
message("${MY_LIST}") 
```

```
set(MY_LIST These are separate arguments)
list(REMOVE_ITEM MY_LIST "separate")            # Removes "separate" from the list
message("${MY_LIST}")                           # Prints: These;are;arguments
```

```
foreach(ARG These are separate arguments)
    message("${ARG}")                           # Prints each word on a separate line
endforeach()
```



##### **Getting and Sitting Property**

A CMake script defines **targets** using the [`add_executable`](https://cmake.org/cmake/help/latest/command/add_executable.html), [`add_library`](https://cmake.org/cmake/help/latest/command/add_library.html) or [`add_custom_target`](https://cmake.org/cmake/help/latest/command/add_custom_target.html) commands. Once a target is created, it has **properties** that you can manipulate using the [`get_property`](https://cmake.org/cmake/help/latest/command/get_property.html) and [`set_property`](https://cmake.org/cmake/help/latest/command/set_property.html) commands. Unlike variables, targets are visible in every scope, even if they were defined in a subdirectory. All target properties are strings.

```
add_executable(MyApp "main.cpp")        # Create a target named MyApp

# Get the target's SOURCES property and assign it to MYAPP_SOURCES
get_property(MYAPP_SOURCES TARGET MyApp PROPERTY SOURCES)

message("${MYAPP_SOURCES}")             # Prints: main.cpp
```