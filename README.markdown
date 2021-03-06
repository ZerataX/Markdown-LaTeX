# Markdown-LaTeX
This [Markdown](https://pypi.python.org/pypi/Markdown) extension adds support for inline LaTeX expressions without the need for external images.
The available modes are %TEXT%, $MATH$, and %%PREAMBLE%%.

## Modes
Markdown-LaTeX can technically allow for any sort of LaTeX expression, but there are three main modes that make writing everything much easier.

### %TEXT% mode
The most basic of the modes is %TEXT% mode. Any expression within %TEXT% will be parsed in a basic LaTeX text-mode, e.g. plain. For example, %``Justin Bruce Van Horne''%.

### $MATH$ mode
Math mode is our second basic functionality of Markdown-LaTeX. It automatically puts LaTeX into math mode and allows for inline and multiline expressions. Let's say that we wanted to write [Euler's formula](http://en.wikipedia.org/wiki/Euler's_formula): We would then write $e^{\imath x} = \cos{x} + \imath\sin{x}$.

### %%PREAMBLE%% mode
Preamble mode is the only "complex" mode. It allows you to add to the preamble of the LaTeX template. So, if there are specific packages or commands you want for the HTML page, then this is where to do it. This is a global modifier and will affect the entire document. I haven't come up with an intuitive design for a per-expression basis.

## Dependencies
Markdown-LaTeX depends on:

- [LaTeX](http://www.latex-project.org/)
- [dvisvgm](https://github.com/mgieseki/dvisvgm)
- [dvipng](http://sourceforge.net/projects/dvipng/)
- [Python Markdown](https://pypi.org/project/Markdown/)

## Installation
You can either copy it into the extensions sub-directory in your markdown folder (ex: /usr/lib/python2.7/site-packages/markdown/extensions/latex.py) or use it locally with the mdx_ prefix. See [Markdown Extensions](https://python-markdown.github.io/extensions/api/) for more details.

## Usage
    markdown -x latex somefile.markdown > somefile.html

## Configuration

This plugin uses dvipng or dvisvgm in order to produce the output images. The arguments
passed to dvipng/dvisvgm are configurable, see [tests/markdown-latex.cfg](tests/markdown-latex.cfg) for an example.
In particular, you may want to adapt the argument passed to the -D option in
order to change output resolution resp. font size, if you use dvipng.

You can change between dvipng and dvisvgm in you markdown-latex.cfg under the [general] section, the default is dvisvgm.
```
[general]
mode = png
```

You may also change the delimiters used for text, math and preamble mode within
the configuration file, see [tests2/markdown-latex.cfg](tests2/markdown-latex.cfg). When running this plugin
on existing text you need to escape all occurrences of % and $. Changing
delimiters may reduce this effort.




----

## How does it work?
The LaTeX extension will search for either $text$ or %text% expressions. For each expression, it generates a tex file that is parsed by latex and then run through dvipng/dvisvgm. The data is encoded via base64 and then inlined.  A cache file (latex.cache) is used to store all expressions and their base64 counterparts. This is to prevent latex from being run each time.

----

## Suggestions/Improvements:
- [Geremy Condra](https://github.com/debatem1)
- [Jabba Laci](https://github.com/jabbalaci)
- [Stefan Huber](https://github.com/shuber2)
