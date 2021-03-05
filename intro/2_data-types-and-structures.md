<!--
https://link-springer-com.ezproxy.unal.edu.co/chapter/10.1007/978-1-4842-5190-4_2
--><
# Data Types and Structures

Julia natively provides a fairly complete and hierarchically organized set of predefined types (especially the numerical ones). These are either scalar—like integers, floating-point numbers, and chars,—or container-like structures able to hold other objects—like multidimensional arrays, dictionaries, sets, etc.

In this chapter, we discuss them, and in the Chapter  4, where we cover Julia custom types, we consider their hierarchical organization.

Every value (even the primitive ones) has its own unique type. By convention types start with a capital letter, such as Int64 or Bool. Sometimes (such as for all container-like structures and some non-container ones), the name of the type is followed by other parameters inside curly brackets, like the types of the contained elements or the number of dimensions. For example, Array{Int64,2} would be used for a two-dimensional array of integers.

In Julia terminology, these are referred as to parametric types. In this book, we will use T as a placeholder to generically indicate a type.

There is no division between object and non-object values. All values in Julia are true objects having a type. Only values, not variables, have types. Variables are simply names bound to values. The :: operator can be used to attach type annotations to expressions and variables in programs. There are two primary reasons to do this:

- As an assertion to help confirm that your program works the way you expect.

- To provide extra type information to the compiler, which can then, in some cases, improve performance.

## 2.1 Simple Types (Non-Containers)

Individual characters are represented by the Char type, e.g. a = 'a' (Unicode is fully supported). Boolean values are represented by the Bool type, whose unique instances are true and false.

Open image in new window In Julia, single and double quotes are not interchangeable. Double quotes produce a char (e.g., x = 'a'), whereas single quotes produce a string (e.g., x = "a").

While the Boolean values true and false in a integer context are automatically cast and evaluated as 1 and 0, respectively, the opposite is not true: if 0 [...] end would indeed rise a non-Boolean (Int64) used in Boolean context TypeError.

The “default” integer type in Julia is Int64 (there are actually 10 different variants of integer types), and it is able to store values between -2^63 and 2^63-1. Similarly, the “default” floating-point type is Float64. Complex numbers (Complex{T}) are supported through the global constant im, representing the principal square root of -1.

A complex number can then be defined as a = 1 + 2im. The mathematical focus of Julia is evident by the fact that there is a native type even for exact ratios of integers, Rational{Int64}, whose instances can be constructed using the // operator:

```julia
a = 2 // 3
```

### 2.1.1 Basic Mathematic Operations

All standard basic mathematical arithmetic operators are supported in the obvious way (+ , - , * , /). To raise a number to a power, use the  ̂ operator (e.g., a = 3^2). Natural exponential expressions (i.e., with the Euler’s number e as a base) are created with a = exp(b) or by using the global constant ℯ (This is not the normal letter e, but the special Unicode symbol for the Euler’s number: type Open image in new window in the REPL to obtain it or use MathConstants.e.). Integer divisions are implemented with the ÷ operator (Open image in new window) and their remainders are given using the “modulo” % operator, as follows:

```julia
a = 3 % 2
```

The pi constant is available as a global constant pi or π (Open image in new window).
