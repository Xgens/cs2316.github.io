% Introduction to Python

# Introduction to Python

<center>
<img src="http://imgs.xkcd.com/comics/python.png"/>
</center>

[http://xkcd.com/353/](http://xkcd.com/353/)

# The Python Language

- Python is a general-purpose programming language, meaning you can write any kind of program in Python.1

    - The opposite of a general purpose language is a domain-specific language, which is designed for one kind of application. Later we’ll learn a domain-specific langauge called SQL which is just for manipulating relational databases.

- Python is interpreted, meaning you can run programs directly after you write them; you don’t have to compile programs to some intermediate form for the operating system or a virtual machine to execute.

The coolest thing about Python ...

# The Python Name

<center>
![By BBC - http://www.bbc.co.uk/comedy/guide/articles/m/gallery/montypythonsflyi_1299002137_2.shtml, released for free downloadoriginally listed differently, when i sent an inquiering e-mail i got the response back that I had inquired about a promotional photograph, so have relisted it, https://en.wikipedia.org/w/index.php?curid=6130072](Flyingcircus_2.jpg)
</center>

Python was named for Monty Python, of which Python’s creator, Guido van Rossum, is a big fan.

# The `python` Program

Practically speaking, Python is a program on your computer that interprets Python programs and statements.

- You can ask `python3` a question without running any Python code. For example, this is how you ask which version of Python is installed (Note: the `$` character is the command prompt in the Unix Bash shell. The Windows command prompt is `C:\>`.):

    ```Python
    $ python --version
    Python 3.5.2 :: Continuum Analytics, Inc.
    ```

  If you get some other response, like command not found, then you haven’t properly installed Python.

# Executing Python Code

- You can run a Python program, which has a .py extension by convention:

    ```sh
    $ python myprogram.py
    ```

- Or you can invoke the interactive Python shell (sometimes called REPL for "Read-Eval-Print Loop"):

    ```sh
    $ python3
    Python 3.5.2 |Continuum Analytics, Inc.| (default, Jul  2 2016, 17:53:06)
    [GCC 4.4.7 20120313 (Red Hat 4.4.7-1)] on linux
    Type "help", "copyright", "credits" or "license" for more information.
    >>>
    ```

    To exit the Python shell type Ctrl-D on Unix, or Ctrl-Z on Windows.

# Hello, Python

Since Kernighan and Ritchie's "The C Programming Language" it's customary for your first program in a new language to be "Hello, world!"

- Open your text editor, paste the following code into a buffer (or tab or window or whatever your editor calls it), and save it as `hello.py`:

    ```Python
    print("Hello, world!")
    ```

- Then open your command shell (terminal on Unix or CMD.exe on Windows), go to the directory where you saved `hello.py` and enter:

    ```sh
    $ python3 hello.py
    ```

    Hello, world! will be printed to the console on the next line.

# Interpreting Python Programs

What happens when we enter `python3 hello.py` at an operating system command shell prompt?

1. `python3` tells the OS to load the Python interpreter into memory and run it. `python3` is the name of an executable file on your hard disk which your OS can find because its directory is on the `PATH`
2. We invoke `python3` with a *command line argument*, which `python3` reads after it starts running
3. Since the command line argument was the name of a file (`hello.py`), the `python3` loads the file named by the argument and executes the Python code in it.

A Python program, or script, is just a sequence of Python statements and expressions.

# The Python REPL

Invoke the Python interactive shell by entering python3 at your command shell’s prompt without any arguments and type in the same line we put in hello.py:

```sh
$ python3
Python 3.5.2 |Continuum Analytics, Inc.| (default, Jul  2 2016, 17:53:06)
[GCC 4.4.7 20120313 (Red Hat 4.4.7-1)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

`>>>` is the command prompt for the Python REPL.

- REPL stands for **R**ead **E**val **P**rint **L**oop -- **R**ead an expression or statement at the command prompt, **E**valuate the expression or execute the statement, **P**rint the result to the console, **L**oop back to **R**ead step

We’ll spend a lot of time in the REPL.
