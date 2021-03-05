
<!-- https://link-springer-com.ezproxy.unal.edu.co/chapter/10.1007/978-1-4842-5190-4_1 
primer capitulo

-->

<!-- https://www.programmer-books.com/wp-content/uploads/2019/04/Beginning-Julia-Programming.pdf
Libro completo
-->
# Getting Started

1.1 Why Julia?

With so many programming languages available, why create yet another one? Why invest the time to learn Julia? Is it worth it?

One of the main arguments in favor of using Julia is that it contributes to improving a trade-off that has long existed in programming—fast coding versus fast execution.

On the one side, Julia allows the developer to code in a dynamic, high-level language similar to Python, R, or MATLAB, interacting with the code and having powerful expressivity (see Chapter  6, for example).

On the other side, with minimum effort, developers can write programs in Julia that run (almost) as fast as programs written in C or FORTRAN.

Wouldn’t it be better, though, to optimize existing languages, with their large number of libraries and established ecosystems, rather than create a new language from scratch?

Well, yes and no. Attempts to improve runtime execution of dynamic languages are numerous. PyPy (https://pypy.org), Cython (https://cython.org), and Numba (https://numba.pydata.org) are three notable examples for the Python programming language. They all clash with one fact: Python (and, in general, all the current dynamic languages) was designed before the recent development of just-in-time (JIT) compilers, and hence it offers features that are not easy to optimize. The optimization tools either fail or require complex workarounds in order to work.

Conversely, Julia has been designed from the ground up to work with JIT compilers, and the language features—and their internal implementations—have been carefully considered in order to provide the programmer with the expected productivity of a modern language, all while respecting the constraints of the compiler. The result is that Julia-compliant code is guaranteed to work with the underlying JIT compiler, producing in the end highly optimized compiled code.

Open image in new window The Shadow Costs of Using a New Language
If it is true that the main “costs” of using a new language relate to learning the language and having to abandon useful libraries and comfortable, feature-rich development editors that you are accustomed to, it is also true that in the Julia case these costs are mitigated by several factors:

    The language has been designed to syntactically resemble mainstream languages (you’ll see it in this book!). If you already know a programming language, chances are you will be at ease with the Julia syntax.

    Julia allows you to easily interface your code with all the major programming languages (see Chapter  7, “Interfacing Julia with Other Languages”), hence reusing their huge sets of libraries (when these are not already ported to Julia).

    The development environments that are available—e.g., Juno (https://junolab.org), IJulia Jupiter kernel (https://github.com/JuliaLang/IJulia.jl), and VSCode Julia plugin (https://github.com/JuliaEditorSupport/julia-vscode)—are frankly quite cool, with many common features already implemented. They allow you to be productive in Julia from the first time you code with it.

Apart from the breakout in runtime performances from traditional high-level dynamic languages, the fact that Julia was created from scratch means it uses the best, most modern technologies, without concerns over maintaining compatibility with existing code or internal architectures. Some of the features of Julia that you will likely appreciate include built-in Git-based package manager, full code introspection, multiple dispatches, in-core high-level methods for parallel computing, and Unicode characters in variable names (e.g., Greek letters).

Thanks to its computational advantages, Julia has its natural roots in the domain of scientific, high-performance programming, but it is becoming more and more mature as a general purpose programming language. This is why this book does not focus specifically on the mathematical domain, but instead develops a broad set of simple, elementary examples that are accessible even to beginner programmers.
1.2 Installing Julia

Julia code can be run by installing the Julia binaries for your system available in the download section (http://julialang.org/downloads/) of the Julia Project website (https://julialang.org).

The binaries ship with a Julia interpreter console (aka, the “REPL”—Read, Eval, Print, Loop), where you can run Julia code in a command-line fashion.

For a better experience, check out an Integrated Development Environment, for example, Juno (http://junolab.org/) an IDE based on the Atom (https://atom.io) text editor, or IJulia (https://github.com/JuliaLang/IJulia.jl), the Julia Jupiter (http://jupyter.org/) backend.
Detailed setup instructions can be found on their respective sites, but in a nutshell, the steps are pretty straightforward.

    For Juno:

        Install the main Julia binaries first.

        Download, install, and open the Atom text editor (https://atom.io).

        From within Atom, go to the Settings ➤ Install panel.

        Type uber-juno into the search box and press Enter. Click the Install button on the package with the same name.
    For IJulia:

        Install the main Julia binaries first.

        Install the Python-based Jupyter Notebook server using the favorite tools of your OS (e.g., the Package Manager in Linux, the Python spip package manager, or the Anaconda distribution).

        From a Julia console, type using Pkg; Pkg.update();Pkg.add("IJulia");Pkg.build("IJulia").

        The IJulia kernel is now installed. Just start the notebook server and access it using a browser.

You can also choose, at least to start with, not to install Julia at all, and try instead one of the online computing environments that support Julia. For example, JuliaBox (https://juliabox.com/), CoCalc (https://cocalc.com/doc/software-julia.html), Nextjournal (https://nextjournal.com), and Binder (https://mybinder.org).
Open image in new window Some tricks for Juno and IJulia

    Juno can:

        Enable block selection mode with Open image in new window.

        Run a selection of code by selecting it and either selecting Run Block or typing Open image in new window on Windows and Linux or Open image in new window on Mac.

        Comment/uncomment a block of code with Open image in new window (Windows and Linux) or Open image in new window (Mac).
    IJulia:

        Check out the many keyboard shortcuts available from Help ➤ Keyboard Shortcuts.

        Need to run Julia in a computational environment for a team or a class? Use JupyterHub (https://github.com/jupyterhub/jupyterhub), the multi-user solution based on Jupyter.

1.3 Running Julia
There are many ways to run Julia code, depending on your needs:

    1.

    Julia can run interactively in a console. Start julia to obtain the REPL console, and then type the commands there (type exit() or use CTRL+D when you are finished).
     
    2.

    Create a script, i.e. a text file ending in .jl, and let Julia parse and run it with julia myscript.jl [arg1, arg2,..].Script files can also be run from within the Julia console. Just type include("myscript.jl").
     
    3.

    In Linux or on MacOS, you can instead add at the top of the script the location of the Julia interpreter on your system, preceded by #! and followed by an empty row, e.g. #!/usr/bin/julia (You can find the full path of the Julia interpreter by typing which julia in a console.). Be sure that the file is executable (e.g., chmod +x myscript.jl).

    You can then run the script with ./myscript.jl.
     
    4.

    Use an Integrated Development Environment (such as those mentioned), open a Julia script, and use the run command specific to the editor.
     

You can define a global (for all users of the computer) and local (for a single user) Julia file that will be executed at any startup, where you can for example define functions or variables that should always be available. The location of these two files is as follows:

    Global Julia startup file: [JULIA_INSTALL_FOLDER]\etc\julia\startup.jl (where JULIA_INSTALL_FOLDER is where Julia is installed)

    Local Julia startup file: [USER_HOME_FOLDER]\.julia\config\startup.jl (where USER_HOME_FOLDER is the home folder of the local user, e.g. %HOMEPATH% in Windows and ~ in Linux)

Remember to use the path with forward slashes ( / ) with Linux. Note that the local config folder may not exist. In that case, just create the config folder as a .julia subfolder and start the new startup.jl file there.

Open image in new window Julia keeps all the objects created within the same work session in memory. You may sometimes want to free memory or “clean up” your session by deleting no longer needed objects. If you want to do this, just restart the Julia session (you may want to use the trick mentioned at the end of Chapter  3) or use the Revise.jl (https://github.com/timholy/Revise.jl) package for finer control.

You can determine which version of Julia you are using with the versioninfo() option (within a Julia session).
1.4 Miscellaneous Syntax Elements

Julia supports single-line ( # ) and multi-line ( #= [...] =# ) comments. Multi-line comments can be nested and appear anywhere in the line:
println("Some code..")       JULIA
#=
  Multiline comment
  #= nested multiline comment =#
  Still a comment
=#
println(#= A comment in the middle of the line =# "This is a code") # Normal single-line comment

You don’t need to use semicolons to indicate the end of a statement. If they’re used, semicolons will suppress the command output (this is done automatically in scripting mode). If the semicolon is used alone in the REPL, it allows you to switch to the OS command shell prompt in order to launch a system-wide command.

Blocks don’t need to be surrounded by parentheses, but they do require the keyword end at the close.

Open image in new window While indentation doesn’t carry any functional meaning in the language, empty spaces sometimes are important. For example, function calls must uses parentheses with the inputs strictly attached to the function name, e.g.:

println (x)   # rise an ERROR      TEXT

println(x)    # OK

In Julia, variable names can include a subset of Unicode symbols, allowing a variable to be represented, for example, by a Greek letter.

In most Julia development environments (including the console), to type a Greek letter, you use a LaTeX-like syntax. This involves typing \, then the LaTeX name for the symbol (e.g. \alpha for α), and then pressing Tab to confirm. Using LaTeX syntax, you can also add subscripts, superscripts, and decorators.

All the following are valid, if not crazy, variable names: x1, x̃, α, y1, y(a+b), y2, Open image in new window, and Open image in new window.

Note, however, that while you can use y2 as a variable name, you can’t use 2y, as the latter is automatically interpreted as 2 * y. Together with Unicode, this greatly simplifies the transposition in computer code of mathematical equations.

If you come from a language that follows a zero-indexing standard (such as C or Python), one important point to remember is that Julia arrays are one-based indexed (counting starts from 1 and not 0). There are ways to override this behavior, but in many cases doing so probably would do more harm than good.
1.5 Packages

Julia developers have chosen an approach where the core of Julia is relatively light, and additional functionality is usually provided by external “packages”.

Julia binaries ship with a set of these packages (think to it as a “Standard Library”) and a powerful package manager that is able to download (typically directly from GitHub repositories), pre-compile, update, and solve dependencies, all with a few simple commands.

While registered packages can be installed simply by using their name, unregistered packages need their source location to be specified. At the time of this writing, over 2,400 registered packages have been published.

Knowing how packages work is essential to efficiently working in Julia, and this is why I have chosen to introduce package management early in the book and complement the book with a discussion of some common packages.
1.5.1 Using the Package Manager
There are two ways to access package management features, interactively and as an API from within other Julia code:

    The interactive way is to type ] in the REPL console to enter a “special” pkg mode. The prompt will then change from julia> to (vX.Y) pkg>, where vX.Y is the current Julia version.

    You can then run any package manager commands or go back to the normal interpreter mode with BACKSPACE.

    The API way is to import the pkg module into your code (using Pkg) and then run Pkg.command(ARGS). Obviously, nothing inhibits you from using the API approach in an interactive session, but the special package mode has tab completion and other goodies that make it more comfortable to use.

    Note that the two interfaces are not 100% consistent, with the API interface being slightly more stringent.

Some of the useful package commands are explained in the following list:

    status: Retrieves a list (name and version) of the locally installed packages.

    update: Updates the local index of packages and all the local packages to the latest version.

    add pkgName: Automatically downloads and installs a given package. For multiple packages use add Pkg1 Pkg2 or Pkg.add(["Pkg1","Pkg2"]).

    add pkgName#master, add pkgName#branchName, or add pkgName#vX.Y.Z: Checks out the master branch of a given package, a specific branch, or a specific release, respectively.

    free pkgName: Returns the package to the latest release.

    rm pkgName: Removes a package and all its dependent packages that have been installed automatically only for it.

    add git@github.com:userName/pkgName.jl.git: Checks out a non-registered package from a Git repository (here, it’s GitHub).

1.5.2 Using Packages
To access the functionalities of a package, you need to either use or import it. The difference is as follows:

    Using a package allows you to access the package functions directly. Just include a using mypackage statement in the console or at the beginning of the script.

    Importing a package does the same, but helps in keeping the namespace clean, as you need then to refer to the package functions using their full names, as myPkg.myFunction. You can use aliases or choose to import only a subset of functions (that you can then access directly).

For example, to access the function plot(), which is available in the package Plots, you can do the following (see the “Plotting” section in Chapter  9 for specific plotting issues):

    Access the package function directly with using myPackage :

    using Plots      JULIA
    plot(rand(4,4))

    Access the package functions using their full names with import myPackage :

    import Plots      JULIA
    const pl = Plots # This (optionally) creates an an alias, equivalent to Python `import Plots as pl`. Declaring it constant may improves the performances.
    pl.plot(rand(4,4)) # `Equivalent to Plots.plot(rand(4,4))`

    Access the package functions directly with import myPackage:myfunction :

    import Plots: plot # We can import multiplefunctions at once using commas      JULIA
    plot(rand(4,4))

Finally, you can also include any Julia source files using this line:
include("MyFile.jl") :

When that line runs, the included file is completely ran (not only parsed) and any symbol defined there becomes available in the scope (the region of code within which a variable is visible) relative to where the include was called.

You can read more about packages in the relevant section (https://julialang.github.io/Pkg.jl/v1/) of the Julia documentation, or by typing help or help COMMAND in pkg mode to get more details on the package manager commands.

Open image in new window Across this book, I refer to several packages, either in the standard library or third-party packages. When I state that a given function belongs to a given package, remember to add using PackageName in order to run the code in the examples (I will not repeat this each time).
1.6 Help System

Julia comes with an integrated help system that retrieves usage information for most functions directly from the source code. This is true also for most third-party packages.

Typing ? in the console leads to the Julia help system, and the prompt changes to help?>. From there, you can search for the function’s API.

Open image in new window In non-interactive environment like IJulia notebooks, you can use ?search_term to access the documentation.

In Juno, you can right-click to open the contextual menu and choose Show Documentation to bring up documentation for the object.

If you don’t remember the function name exactly, Julia is kind enough to return a list of similar functions.
While the actual content returned may vary, you can expect to see the following information for each function you query:

    Its signature

    One-line description

    Argument list

    Hints to similar or related functions

    One or more usage examples

    A list of methods (for functions that have multiple implementations)
