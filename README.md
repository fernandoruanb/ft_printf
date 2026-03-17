
<p align="center">
  <img src="https://github.com/ayogun/42-project-badges/raw/main/covers/cover-ft_printf.png" alt="ft_printf cover" width="100%">
</p>

<h1 align="center">
  <br>
  <a href="https://github.com/SEU_USUARIO/ft_printf">
    <img src="https://github.com/ayogun/42-project-badges/raw/main/badges/ft_printfe.png" alt="ft_printf badge" width="200">
  </a>
  <br>
  ft_printf
  <br>
</h1>

<h4 align="center">
  A custom formatted output function built from scratch in <a href="https://www.c-language.org/" target="_blank">C</a>.
</h4>

<p align="center">
  <img src="https://img.shields.io/badge/Final%20Score-100%2F100-00C853?style=for-the-badge" alt="Final Score 100/100">
  <img src="https://img.shields.io/badge/Language-C-00599C?style=for-the-badge&logo=c" alt="Language C">
  <img src="https://img.shields.io/badge/Build-Makefile-orange?style=for-the-badge" alt="Build Makefile">
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge" alt="Status Completed">
</p>

<p align="center">
  <a href="#about-the-project">About</a> •
  <a href="#variadic-functions">Variadic Functions</a> •
  <a href="#how-it-works">How It Works</a> •
  <a href="#supported-conversions">Supported Conversions</a> •
  <a href="#how-to-use">How To Use</a> •
  <a href="#team">Team</a>
</p>

---

<!-- Replace with your own GIF -->
<!-- ![demo](./assets/ft_printf-demo.gif) -->

## About the Project

**ft_printf** appears in the early stages of the journey at **École 42** as a project designed to make formatted output truly understandable.

A simple way to understand it is to imagine **ft_printf as a waiter**.

At the beginning of the C journey, we usually build small output functions such as:

- `ft_putchar` → prints a single character
- `ft_putnbr` → prints a number
- `ft_putstr` → prints a full string

Each function has one specific responsibility.

But then a natural question appears:

> What if we want a single function capable of organizing and printing many different types of data?

Instead of manually calling several output functions, it is much more powerful to create **one central system** capable of interpreting a format string and dispatching each value to the correct internal handler.

That is exactly what **ft_printf** does.

Like a waiter in a restaurant:

1. It receives the order.
2. It interprets what was requested.
3. It forwards each request to the right place.

In the same way, **ft_printf receives a format string**, parses it, identifies each conversion specifier, and calls the correct internal function to print the requested data.

---

## Variadic Functions

One of the most important concepts introduced by **ft_printf** is the use of **variadic functions**.

Unlike regular functions, which receive a fixed number of parameters, variadic functions can handle **an undefined number of arguments**.

To make that possible, C provides the following tools:

- `va_list`
- `va_start`
- `va_arg`
- `va_end`

These mechanisms allow us to traverse the argument list dynamically and extract each value according to the format specifier currently being parsed.

This is one of the core ideas behind how `printf` works internally.

---

## How It Works

The logic of **ft_printf** is simple in concept, but very powerful in practice.

Just like the original `printf`, the function must **return the total number of characters printed**.

### 1. Variadic argument initialization

First, the variadic list is initialized:

```c
va_list args;
va_start(args, format);
````

At that point, the function gains access to all extra arguments passed by the user.

### 2. Parsing the format string

The format string is then analyzed character by character.

Two situations may happen:

* A **regular character** is found
  It is printed directly, and the total printed character count is incremented.

* A **special character `%`** is found
  This means a conversion specifier is coming next.

### 3. Detecting the specifier

Once `%` is found, the next character is checked to determine what must be printed.

### 4. Calling the correct handler

If the specifier is `%s`, the string handler is called.
If it is `%d`, the integer handler is called.
If it is `%x`, the hexadecimal handler is called, and so on.

At that moment, `va_arg(args, type)` is used to fetch the next value from the argument list.

### 5. Printing and counting

Each handler:

1. receives the value
2. processes it if needed
3. prints it
4. updates the total character counter

### 6. Final return

After the whole format string has been parsed and everything has been printed, the function returns the total number of printed characters.

```c
return total_printed_chars;
```

---

## Supported Conversions

The mandatory version of **ft_printf** supports the classic conversion specifiers below:

| Specifier | Meaning               |
| --------- | --------------------- |
| `%c`      | character             |
| `%s`      | string                |
| `%p`      | pointer address       |
| `%d`      | signed decimal        |
| `%i`      | signed integer        |
| `%u`      | unsigned decimal      |
| `%x`      | lowercase hexadecimal |
| `%X`      | uppercase hexadecimal |
| `%%`      | literal percent sign  |

---
<html>
<img src="https://cdn.pixabay.com/photo/2016/10/27/06/38/tea-time-1773531_1280.png"\>
</html>

## The "Waiter" Analogy

The waiter analogy is a very intuitive way to visualize the project:

1. The client places the order.
2. The waiter reads and understands it.
3. The waiter identifies what is needed.
4. The waiter sends each request to the proper area.
5. The order is delivered.
6. In the end, the waiter knows how many items were served.

That is exactly the role of **ft_printf**:

It acts as a central dispatcher that interprets instructions and forwards each printing task to the right internal function.

---

## How To Use

Compile the project with:

```bash
make
```

Once compiled, you can link your implementation with a test program containing `main`.

### Example using the project source files directly

```bash
cc -Wall -Wextra -Werror ft_printf.c convert_*.c ft_strlen.c handle*.c parse*.c print*.c yourProgram.c -I . -o myPrintf
```

Then you can use your function like this:

```c
ft_printf("Hello World, %s\n", "Fernando");
```

### Example using a generated static library

If your Makefile generates a library such as `libftprintf.a`, you can compile like this:

```bash
cc -Wall -Wextra -Werror yourProgram.c libftprintf.a -I . -o myPrintf
```

---

## Team

**ft_printf** is an individual project at **École 42**.

It was fully developed by me.

---

## Final Note

More than reproducing a famous standard function, **ft_printf** was an opportunity to understand formatted output from the inside.

It transformed something that once looked magical into something concrete:

* parsing
* dispatching
* variadic arguments
* modular printing
* character counting
* low-level formatted output design

For me, this project marked an important step forward in understanding how C really works under the hood.

